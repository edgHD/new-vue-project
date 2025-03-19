<template>
    <!-- Form for adding a new friend contact -->
    <form @submit.prevent="submitData">
        <!-- Name input field -->
        <div>
            <label>Name</label>
            <input type="text" placeholder="Name" v-model="enteredName" required/>
        </div>
        
        <!-- Phone number input field -->
        <div>
            <label>Phone Number</label>
            <input type="tel" placeholder="Phone Number" v-model="enteredPhone" required/>
        </div>
        
        <!-- Email input field -->
        <div>
            <label>Email</label>
            <input type="email" placeholder="Email" v-model="enteredEmail" required/>
        </div>
        
        <!-- Submit button -->
        <div>
            <button>Add Contact</button>
        </div>
    </form>
</template>
<script>
export default {
    // Declares the custom event this component can emit to its parent
    emits: ['add-contact'],
    
    // Component's internal state to track form input values
    data() {
        return {
            enteredName: '', // Stores the entered name
            enteredPhone: '', // Stores the entered phone number
            enteredEmail: '' // Stores the entered email
        }
    },
    
    methods: {
        // Handles form submission
        submitData() {
            // Emits an event to the parent component with the entered data
            this.$emit('add-contact',
                this.enteredName,
                this.enteredPhone,
                this.enteredEmail
            );
            //Deletes entered input after submission
            this.enteredName = '';
            this.enteredPhone = '';
            this.enteredEmail = '';
        }
    }
};
</script>
<style scoped>
/* Form container styling */
form {
    background-color: #ffb84d; /* Orange background matching FriendContact */
    border: 1px solid #dd9300; /* Darker orange border */
    border-radius: 10px; /* Rounded corners */
    padding: 20px; /* Space inside the form */
    max-width: 600px; /* Maximum width */
    margin: 20px auto; /* Centers form horizontally with margin */
    font-family: Arial, sans-serif; /* Font style */
}

/* Label styling */
form label {
    display: block; /* Makes labels appear on their own line */
    font-weight: bold; /* Bold text */
    color: #000; /* Black text color */
    margin-bottom: 5px; /* Space below each label */
    text-align: left; /* Left-aligns text */
}

/* Input field styling */
form input {
    width: 60%; /* Width relative to container */
    padding: 10px; /* Space inside input fields */
    border: 1px solid #dd9300; /* Darker orange border */
    background-color: #ffcc66; /* Light orange background */
    border-radius: 5px; /* Rounded corners */
    margin-bottom: 15px; /* Space below each input */
    font-size: 1rem; /* Font size */
}

/* Submit button styling */
form button {
    display: block; /* Makes button a block element */
    background-color: #76ff05; /* Green background */
    color: darkblue; /* Dark blue text */
    border: none; /* No border */
    padding: 10px 15px; /* Space inside button */
    border-radius: 5px; /* Rounded corners */
    cursor: pointer; /* Hand cursor on hover */
    font-size: 1rem; /* Font size */
    transition: 0.2s; /* Smooth transition for hover effects */
    margin: 15px auto 0; /* Centers button horizontally with margin */
    width: 25%; /* Width relative to container */
}

/* Hover effect for submit button */
form button:hover {
    background-color: #5bca00; /* Darker green on hover */
    color: blue; /* Brighter blue text on hover */
    transition: 0.2s; /* Smooth transition */
}

/* Container for form elements */
form div {
    display: flex; /* Enables flexbox layout */
    justify-content: space-between; /* Spreads content across available space */
    align-items: stretch; /* Stretches items to fill container height */
    margin-bottom: 15px; /* Space below each container */
}
</style>
