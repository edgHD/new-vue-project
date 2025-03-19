<template>
    <!-- Represents a single friend's contact information -->
    <li>
        <!-- Displays friend's name and adds a heart emoji if marked as favorite -->
        <h2>{{ name }} {{ isFavorite ? "❤️" : "" }}</h2>

        <!-- Button to toggle visibility of contact details, changes class and text based on current state -->
        <button :class="!detailsAreVisible ? 'show-details' : 'hide-details'" @click="toggleDetails">
            {{ !detailsAreVisible ? "Show" : "Hide" }} Details
        </button>

        <!-- Button to toggle favorite status, changes class and text based on current state -->
        <button :class="!isFavorite ? 'add-favorite' : 'delete-favorite'" @click="toggleFavorite">
            {{ !isFavorite ? "Add to" : "Delete from" }} favorite
        </button>

        <!-- Conditionally displays additional details (phone and email) when detailsAreVisible is true -->
        <ul v-if="detailsAreVisible">
            <li><strong>Phone:</strong> {{ phoneNumber }}</li>
            <li><strong>Email:</strong> {{ emailAddress }}</li>
        </ul>
        
        <!-- Button to delete this friend's contact, emits 'delete' event with friend's ID -->
        <button class="delete-friend" @click="this.$emit('delete', id)">🗑️</button>
    </li>
</template>
<script>
export default {
    // Props define the data that can be passed to this component from its parent
    props: {
        id: {
            type: String,
            required: true // Friend's unique identifier is mandatory
        },
        name: {
            type: String,
            required: true // Friend's name is mandatory
        },
        phoneNumber: {
            type: Number,
            required: true // Friend's phone number is mandatory
        },
        emailAddress: {
            type: String,
            required: true // Friend's email address is mandatory
        },
        isFavorite: {
            type: Boolean,
            required: false, // Favorite status is optional
            default: false // Default value if not provided
        }
    },
    
    // Declares the custom events this component can emit to its parent
    emits: ['toggle-favorite', 'delete'],
    
    // Alternative way to validate emitted events (commented out)
    // emits: {
    //     'toggle-favorite': function(id) {
    //         if (id) {
    //             return true
    //         } else {
    //             console.warn('ID is missing!')
    //         }
    //     }
    // },
    
    // Component's internal state
    data() {
        return {
            detailsAreVisible: false // Controls whether details are shown or hidden
        };
    },
    
    methods: {
        // Toggles the visibility of contact details
        toggleDetails() {
            this.detailsAreVisible = !this.detailsAreVisible;
        },
        
        // Emits an event to the parent component to toggle favorite status
        toggleFavorite() {
            this.$emit('toggle-favorite', this.id);
        }
    }
};
</script>
<style scoped>
/* Styling for each friend contact card */
li {
    text-align: center; /* Centers text within the list item */
    background-color: #ffb84d; /* Orange background color */
    border: 1px solid #dd9300; /* Darker orange border */
    border-radius: 8px; /* Rounded corners */
    padding: 15px; /* Space inside the card */
    margin: 10px 0; /* Vertical spacing between cards */
    font-family: Arial, sans-serif; /* Font style */
}

/* General button styling */
button {
    margin: 0 5px; /* Horizontal spacing between buttons */
}

/* Friend's name styling */
h2 {
    margin: 0; /* Removes default margin */
    font-size: 1.5rem; /* Font size */
    color: black; /* Text color */
    text-align: center; /* Centers text */
}

/* "Show Details" button styling */
.show-details {
    background-color: #76ff05; /* Green background */
    color: darkblue; /* Text color */
    border: none; /* No border */
    padding: 10px 15px; /* Inner spacing */
    border-radius: 5px; /* Rounded corners */
    cursor: pointer; /* Hand cursor on hover */
    font-size: 1rem; /* Font size */
    margin-top: 10px; /* Space above button */
    transition: 0.2s; /* Smooth transition for hover effects */
}

/* Hover effect for "Show Details" button */
.show-details:hover {
    background-color: #5bca00; /* Darker green on hover */
    color: blue; /* Brighter blue text on hover */
    transition: 0.2s; /* Smooth transition */
}

/* "Hide Details" button styling */
.hide-details {
    background-color: #ff0505; /* Red background */
    color: darkblue; /* Text color */
    border: none; /* No border */
    padding: 10px 15px; /* Inner spacing */
    border-radius: 5px; /* Rounded corners */
    cursor: pointer; /* Hand cursor on hover */
    font-size: 1rem; /* Font size */
    margin-top: 10px; /* Space above button */
    transition: 0.2s; /* Smooth transition for hover effects */
}

/* Hover effect for "Hide Details" button */
.hide-details:hover {
    background-color: #af0000; /* Darker red on hover */
    color: cyan; /* Cyan text on hover */
    transition: 0.2s; /* Smooth transition */
}

/* "Add to favorite" button styling */
.add-favorite {
    background-color: #fbff05; /* Yellow background */
    color: darkblue; /* Text color */
    border: none; /* No border */
    padding: 10px 15px; /* Inner spacing */
    border-radius: 5px; /* Rounded corners */
    cursor: pointer; /* Hand cursor on hover */
    font-size: 1rem; /* Font size */
    margin-top: 10px; /* Space above button */
    transition: 0.2s; /* Smooth transition for hover effects */
}

/* Hover effect for "Add to favorite" button */
.add-favorite:hover {
    background-color: #acaf00; /* Darker yellow on hover */
    color: blue; /* Brighter blue text on hover */
    transition: 0.2s; /* Smooth transition */
}

/* "Delete from favorite" button styling */
.delete-favorite {
    background-color: #9b05ff; /* Purple background */
    color: darkblue; /* Text color */
    border: none; /* No border */
    padding: 10px 15px; /* Inner spacing */
    border-radius: 5px; /* Rounded corners */
    cursor: pointer; /* Hand cursor on hover */
    font-size: 1rem; /* Font size */
    margin-top: 10px; /* Space above button */
    transition: 0.2s; /* Smooth transition for hover effects */
}

/* Hover effect for "Delete from favorite" button */
.delete-favorite:hover {
    background-color: #5b0097; /* Darker purple on hover */
    color: cyan; /* Cyan text on hover */
    transition: 0.2s; /* Smooth transition */
}

/* Delete friend button styling */
.delete-friend {
    background-color: #444; /* Dark gray background */
    transition: 0.2s; /* Smooth transition for hover effects */
}

/* Hover effect for delete friend button */
.delete-friend:hover {
    background-color: #000; /* Black background on hover */
    transition: 0.2s; /* Smooth transition */
}

/* Styling for the nested unordered list (contact details) */
ul {
    list-style-type: none; /* Removes bullet points */
    padding: 10px 0 0 0; /* Padding only at the top */
    margin: 0; /* Removes default margin */
}

/* Styling for individual contact details */
li ul li {
    margin: 5px 0; /* Vertical spacing between details */
    font-size: 1rem; /* Font size */
    color: #555; /* Gray text color */
    background-color: #ffcc66; /* Lighter orange background */
}

/* Styling for label text (Phone, Email) */
strong {
    font-weight: bold; /* Bold text */
    color: #000; /* Black text color */
}
</style>
