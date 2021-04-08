<script>
  import AddPersonForm from './AddPersonForm.svelte';
  import Modal from './Modal.svelte';

  let showModal = false;
  let toggleModal = () => {
    showModal = !showModal;
  };

  let people = [
    { name: 'yoshi', beltColour: 'black', age: 25, id: 1 },
    { name: 'mario', beltColour: 'orange', age: 45, id: 2 },
    { name: 'luigi', beltColour: 'brown', age: 35, id: 3 },
  ];
  const handleClick = (e, id) => {
    people = people.filter((person) => person.id != id);
    console.log(e);
  };

  const addPerson = (e) => {
    // console.log(e.detail);
    const person = e.detail;
    people = [person, ...people];
    showModal = false;
  };
</script>

<Modal {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} />
</Modal>
<!-- <Modal message="Hey, I am a prop value" isPromo={true} {showModal} /> -->
<main />
<button on:click={toggleModal}>Modal</button>
{#each people as person (person.id)}
  <div>
    <h4>{person.name}</h4>
    {#if person.beltColor === 'black'}
      <p><strong>MASTER NINJA</strong></p>
    {/if}
    <p>{person.age} years old, {person.beltColor} belt.</p>
    <button
      on:click={(e) => {
        handleClick(e, person.id);
      }}>delete</button
    >
  </div>
{:else}
  <p>There are no people to show...</p>
{/each}

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
