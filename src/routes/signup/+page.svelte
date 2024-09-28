<script>
    import { Root } from 'postcss';
    import '../../app.css';
    import { Button } from "bits-ui";
    import { endpoint } from "$lib/index";

    async function submit() {
        try {
            let rawResponse = await fetch(`${endpoint}/user/signup`, {
                method: "POST",
                credentials: "include",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({"username": username})
            })
            let response = await rawResponse.json();
            console.log(response);
        } catch (error) {
            // Not logged in, redirect to home
            window.location.replace(window.location.origin + "/");
        }
    }

    let username = "";

    async function logout() {
        try {
            let rawResponse = await fetch(`${endpoint}/user/logout`, {
                method: "GET",
                credentials: "include",
                headers: {
                    'Accept': 'application/json',
                }
            })
            let response = await rawResponse.json();
            window.location.replace(window.location.origin + "/");
        } catch (error) {
            // Not logged in
        }
    }
</script>
<div class="flex items-center justify-center prose">
    <div class="card bg-neutral text-neutral-content w-96">
        <div class = "flex card-body items-center text-center">
            <h1>Sign Up</h1>
            <div class = "flex flex-col gap-4">
                <label class="input input-bordered flex items-center gap-2">
                    Username:
                    <input type="text" bind:value={username}/>
                </label>
                <Button.Root on:click = {submit} class="btn btn-primary">
                    Submit
                </Button.Root>
            </div>
            
        </div>
    </div>
</div>


