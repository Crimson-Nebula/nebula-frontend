<script>
    import '../app.css';

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
            // Not logged in
        }
    }
</script>

<h1>Nebula</h1>
<button on:click={logout} class="btn">Logout</button>