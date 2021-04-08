<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let name;
  let beltColor;
  let age;
  let skills = [];
  const handleSubmit = () => {
    const person = {
      name,
      beltColor,
      age,
      skills,
      id: Math.random(),
    };
    dispatch('addPerson', person);
  };
</script>

<h3>Add a New Person</h3>
<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder="name" bind:value={name} />
  <!-- <input type="text" placeholder="belt color" bind:value={beltColor} /> -->
  <input type="number" placeholder="age" bind:value={age} />
  <label for="">Skills:</label>
  <input type="checkbox" bind:group={skills} value="fighting" />fighting<br />
  <input type="checkbox" bind:group={skills} value="sneaking" />sneaking<br />
  <input type="checkbox" bind:group={skills} value="running" />running<br />
  <label>Belt Color:</label>
  <select bind:value={beltColor}>
    <option value="black">black</option>
    <option value="orange">orange</option>
    <option value="brown">brown</option>
    <option value="white">white</option>
    <option value="black">black</option>
  </select>
  <button>Add Person</button>
</form>
