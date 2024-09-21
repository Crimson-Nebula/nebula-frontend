<script>

    async function submit() {
        try {
            let rawResponse = await fetch("http://localhost:5000/user/create", {
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
            // Not logged in, redirect to login
            window.location.replace(window.location.origin + "/login");
        }
    }

    let username = "";

    async function logout() {
        try {
            let rawResponse = await fetch("http://localhost:5000/user/logout", {
                method: "GET",
                credentials: "include",
                headers: {
                    'Accept': 'application/json',
                }
            })
            let response = await rawResponse.json();
            console.log(response);
        } catch (error) {
            // Not logged in, redirect to login
            //window.location.replace(window.location.origin + "/login");
        }
    }
</script>

<div>
    <input type="text" bind:value={username} placeholder="Username" />
    <button on:click={submit}>Submit</button>
    <button on:click={logout}>Logout</button>
</div>