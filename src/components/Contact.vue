<script setup>
    import { ref } from "vue";
    import { Notyf } from 'notyf';
    // this is normally added in main/js but since notyf will only be used in Contact.vue, we added it here
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    // This cariable will contain the access key from WEB3FORMS
    const WEB3FORMS_ACCESS_KEY = "25746edd-2888-4a62-ac1c-c0143e7ef1c7";

    // This will contain the subject of the email you will receive when someone submits the contact form
    const subject = "New message from Portfolio Contact Form";

    // The reactive data that will contain the value from the form
    const name = ref("");
    const email = ref("");
    const message = ref("");
    const isLoading =ref(false);

    // Async function for submitting the contact form 
    const submitForm = async () => {

        // this will make the button disabled while running the function 
        isLoading.value = true;

        try {
            // Fetch API is used to send HTTPP requests to the browser
            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                // When using fetch, the data we send to the API must be strigified
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    email: email.value,
                    name: name.value,
                    message: message.value
                })
            })

            // This will convert the json response from the API to JS object
            // With axios, this is done automatically by the package
            const result = await response.json();

            if (result.success) {
                console.log(result);
                isLoading.value = false;
                notyf.success("Message Sent!")
            }
        } catch(e) {
            console.log(e);
            isLoading.value = false;
            notyf.error("Failed to send message. Please try again.")
        }
    }
</script>
<template>
    <!-- contact -->
    <h1 class="text-center my-4 pt-5" id="contact">Contact</h1>
    <div class="contact-section">
        <div class="row align-items-center mt-4">
            <div class="col-md-6 map-container">
                <iframe id="gmap_canvas" src="https://maps.google.com/maps?q=centro%20escolar%20university%20manila&t=&z=13&ie=UTF8&iwloc=&output=embed" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"></iframe>
            </div>
            <div class="col-md-6">
                <form @submit.prevent="submitForm">
                    <div class="mb-3">
                        <input 
                            type="text" 
                            class="form-control contact-form-control"
                            placeholder="First Name M.I. Last Name" 
                            v-model="name"
                        >
                    </div>
                    <div class="mb-3">
                        <input 
                            type="email"
                            class="form-control contact-form-control"
                            placeholder="Email"
                            v-model="email"
                        >
                    </div>
                    <div class="mb-3">
                        <textarea 
                            class="form-control contact-form-control"
                            rows="6" 
                            placeholder="Message" 
                            v-model="message">
                        </textarea>
                    </div>
                    <div class="form-footer">
                        <div class="social-icons">
							<!--<a href="https://www.facebook.com/profile.php?id=100085701498879" id="facebook"><i class="fab fa-facebook"></i></a> -->
                            <a href="https://www.linkedin.com/in/charles-babbage-8291a6211/" id="linkedin"><i class="fab fa-linkedin"></i></a>
                            <a href="https://gitlab.com/cbabbage0991" id="gitlab"><i class="fab fa-gitlab"></i></a>
                            <a href="https://github.com/cbabbage0991" id="github"><i class="fab fa-github"></i></a>
                        </div>
                        <button 
                            type="submit"
                            class="submit-btn pl-5 pr-5"
                            :disabled="isLoading">
                                {{ isLoading ? "Sending..." : "Send Message" }}
                        </button>
                    </div>
                </form>
                
            </div>
        </div>
    </div>
</template>