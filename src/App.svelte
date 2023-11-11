<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetup from "./Meetups/EditMeetup.svelte";

  let meetups = [
    {
      id: "m1",
      title: "Coding Bootcamp",
      subtitle: "Learn to code in 2 hours",
      description:
        "In this meetup, we will have some experts that can teach you how to code",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Caffe_Nero_coffee_bar.jpg/1024px-Caffe_Nero_coffee_bar.jpg",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "l7Y1R@example.com",
      isFavorite: false,
    },
    {
      id: "m2",
      title: "Swim Together",
      subtitle: "Let's go for some swimming",
      description: "We will simply swim some rounds!",
      imageUrl:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/6/69/Aquarium_in_Boston%2C_Massachusetts%2C_1870.jpg/800px-Aquarium_in_Boston%2C_Massachusetts%2C_1870.jpg",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "l7Y1R@example.com",
      isFavorite: false,
    },
  ];

  let editMode;

  function addMeetup(event) {
    const newMeetup = {
      id: Math.random().toString(),
      title: event.detail.title,
      subtitle: event.detail.subtitle,
      description: event.detail.description,
      imageUrl: event.detail.imageUrl,
      address: event.detail.address,
      contactEmail: event.detail.email,
    };

    meetups = [newMeetup, ...meetups];
    editMode = null;
  }

  function togglefavorite(event) {
    const id = event.detail;
    const updatedMeetup = { ...meetups.find((m) => m.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
    const meetupIndex = meetups.findIndex((m) => m.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;
    meetups = updatedMeetups;
  }


  function cancelEdit() {
    editMode = null;
  }


</script>

<Header />

<main>
  <div class="meetup-controls">
    <Button on:click={() => (editMode = "add")} >New Meetup</Button>
  </div>

  <!-- {#if editMode === "add"}
    <EditMeetup />
  {:else}
    <MeetupGrid {meetups} on:togglefavorite={togglefavorite} />
  {/if} -->
  {#if editMode === "add"}
    <EditMeetup on:save={addMeetup} on:cancel={cancelEdit} />
  {/if}
  <MeetupGrid {meetups} on:togglefavorite={togglefavorite} />
</main>

<style>
  main {
    margin-top: 5rem;
  }

  .meetup-controls {
    margin: 1rem;
  }
</style>
