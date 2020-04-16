<script>
  import Modal from "./Modal.svelte";
  import AddPersonForm from "./AddPersonForm.svelte";

  let showModal = false;

  let people = [
    {
      name: "John",
      beltColor: "black",
      skills: [],
      age: 27,
      id: 1
    },
    {
      name: "Carol",
      beltColor: "orange",
      skills: ["sneaking", "running"],
      age: 26,
      id: 2
    },
    {
      name: "Mary",
      beltColor: "white",
      skills: ["fighting"],
      age: 2,
      id: 3
    }
  ];

  const toggleModal = () => {
    showModal = !showModal;
  };

  const handleClick = id => {
    // delete the person from people
    people = people.filter(p => p.id !== id);
  };

  const addPerson = e => {
    people = [e.detail, ...people];
    toggleModal();
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 100%;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<Modal {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
  <button on:click={toggleModal}>Open Modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColor === 'black'}
        <p>
          <strong>MASTER NINJA</strong>
        </p>
      {/if}
      <h6>{person.skills.join(', ')}</h6>
      <p>{person.age} years old, {person.beltColor} belt.</p>
      <button on:click={() => handleClick(person.id)}>delete</button>
    </div>
  {:else}
    <p>There is no people to show...</p>
  {/each}
</main>
