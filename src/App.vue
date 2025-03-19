<template>
  <!-- The main structure of the app is defined here -->
  <body>
    <!-- Header Section -->
    <header>
      <!-- Displays the title of the app -->
      <h1>My Friends</h1>
    </header>
    
    <!-- Section for adding a new friend -->
    <section>
      <!-- Custom component for adding a new friend. Emits an event 'add-contact' when a new contact is added -->
      <new-friend @add-contact="addContact"></new-friend>
    </section>

    <!-- Section for displaying the list of friends -->
    <section>
      <ul>
        <!-- Loops through the 'friends' array and renders a FriendContact component for each friend -->
        <friend-contact 
          v-for="friend in friends" 
          :key="friend.id" 
          :id="friend.id" 
          :name="friend.name"
          :phone-number="friend.phone" 
          :email-address="friend.email" 
          :is-favorite="friend.isFavorite"
          @toggle-favorite="toggleFavoriteStatus" 
          @delete="deleteContact">
        </friend-contact>
      </ul>
    </section>
  </body>
</template>

<script>
// Main Vue component handling the app's data and methods
export default {
  // Data object contains the list of friends
  data() {
    return {
      friends: [
        {
          id: "1", // Unique identifier for each friend
          name: "Edgar", // Friend's name
          phone: "012-345-6789", // Friend's phone number
          email: "edghd@localhost", // Friend's email address
          isFavorite: false, // Indicates whether the friend is marked as favorite
        }
      ],
    };
  },
  methods: {
    // Toggles the favorite status of a friend based on their ID
    toggleFavoriteStatus(friendId) {
      const thisFriend = this.friends.find((friend) => friend.id === friendId);
      thisFriend.isFavorite = !thisFriend.isFavorite; // Switches between true and false
    },
    
    // Adds a new contact to the friends list
    addContact(name, phone, email) {
      const newFriendContact = {
        id: new Date().toISOString(), // Generates a unique ID based on the current timestamp
        name: name, // Name of the new contact
        phone: phone, // Phone number of the new contact
        email: email, // Email address of the new contact
        isFavorite: false // Default value for favorite status (not favorite)
      };
      this.friends.push(newFriendContact); // Adds the new contact to the friends array
    },
    
    // Deletes a contact from the friends list based on their ID
    deleteContact(friendId) {
      this.friends = this.friends.filter((friend) => friend.id !== friendId); // Removes the friend with matching ID
    }
  },
};
</script>

<style scoped>
/* Styling for header section */
header {
  background-color: #b0eb00; /* Light green background */
  text-align: center; /* Centers content horizontally */
  padding: 20px; /* Adds space inside the header */
  border: 1px solid #5d7c00; /* Green border around header */
}

h1 {
  font-family: Arial, sans-serif; /* Sets font style */
  color: black; /* Text color */
  font-size: 2rem; /* Font size */
  margin: 0; /* Removes default margin around heading */
}

/* Styling for unordered list containing friends */
ul {
  list-style-type: none; /* Removes bullets from list items */
  padding: 0; /* Removes padding inside unordered list */
  margin: 20px auto; /* Centers list vertically with margin */
  max-width: 600px; /* Restricts width to make it visually appealing */
}
</style>
