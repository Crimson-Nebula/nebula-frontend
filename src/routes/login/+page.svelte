<script lang="ts">
    import {onMount} from "svelte";
    import '../../app.css';

    function handleCredentialResponse(response: any) {
		let formData = new FormData();
		formData.append("credential", response.credential);
		fetch("http://localhost:5000/user/login", {
			method: "POST",
            credentials: "include",
			body: formData
		})
        .then(response => response.json())
        .then(data => {
            if (data['status'] == "OK") {
                // redirect to home page
                window.location.replace(window.location.origin + "/");
            } else if (data['status'] == "CREATE_USER") {
                // redirect to create user page
                window.location.replace(window.location.origin + "/signup");
            }
        });
    }

    onMount(() => {
        //google is imported from the script loaded in the head
        google.accounts.id.initialize({
            client_id: "358229656846-r8l2ot51j16mt7hdd6g63o9g3p5qo4p1.apps.googleusercontent.com",
            callback: handleCredentialResponse,

			state_cookie_domain: "localhost",
        });
        google.accounts.id.renderButton(
            document.getElementById("buttonDiv"),
            { theme: "filled_black", size: "large", text: "continue_with" }  // customization attributes
        );
        //google.accounts.id.prompt(); // also display the One Tap dialog
    });
</script>

<svelte:head>
    <script src="https://accounts.google.com/gsi/client" async></script>
</svelte:head>

<div class="flex justify-center">
    <div class="prose flex flex-col justify-center p-5">
        <h1 class="inline text-center">Log In</h1>
        <div id="buttonDiv" style="color-scheme: light"></div>
    </div>
</div>

