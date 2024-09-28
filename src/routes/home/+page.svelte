<script lang="ts">
    import {onMount} from "svelte";
    import '../../app.css';

    let posts:any = [];

    async function getFeed() {
        try {
            let rawResponse = await fetch("http://localhost:5000/user/feed", {
                method: "GET",
                credentials: "include",
                headers: {
                    'Accept': 'application/json',
                }
            })
            let response = await rawResponse.json();
            posts = response.posts;
        } catch (error) {
            // Not logged in
        }
    }

    onMount(() => {
        //Call API
    });
    
</script>

<div>
    {#each posts as post}
        <div class="flex justify-center w-75">
            <div class="card bg-base-100 w-100 shadow-xl">
                <div class="card-body items-start text-center">
                    <h2 class="card-title">{post.username}</h2>
                    <p>{post.content}</p>
                    <figure>
                        <img class = "max-w-[450px]" 
                        src="https://img.daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.webp"
                        alt="Shoes" />
                    </figure>
                </div>
            </div>
        </div>
    {/each}
</div>


