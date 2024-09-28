<script lang="ts">
    import { Dialog, Button } from "bits-ui";
    import {fade} from "svelte/transition";
    import '../app.css';

    let content = "";

    let dialogOpen = false;

    //Testing add post
    async function createPost() {

        if (content === "") {
            alert("No content");
            return;
        }

        try {
            let rawResponse = await fetch("http://localhost:5000/post/create", {
                method: "POST",
                credentials: "include",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(
                    {
                        "content": content,
                        "externalUrl": ""
                    })
            });
        } catch (error) {
            // Not logged in, redirect to login
            console.log(error)
            //window.location.replace(window.location.origin + "/login");
        }
        dialogOpen = false;
    }
</script>

<Dialog.Root bind:open={dialogOpen}>
    <Dialog.Trigger class="btn">
        Write Post
    </Dialog.Trigger>
    <Dialog.Portal>
        <Dialog.Overlay
                transition={fade}
                transitionConfig={{ duration: 150 }}
                class="fixed inset-0 z-50 bg-black/80"
        />
        <Dialog.Content class="fixed prose left-[50%] top-[50%] z-50 translate-x-[-50%] translate-y-[-50%] modal-box">
            <Dialog.Title class="flex w-full">
                <h3>Write Post</h3>
            </Dialog.Title>
            <div class="flex justify-center">
                <input type="text" bind:value={content} placeholder="Start writing..." class="input input-bordered w-full" />
            </div>
            <Button.Root on:click = {createPost} class="btn btn-primary">
                Post
            </Button.Root>
            <Dialog.Close class="absolute right-5 top-5 rounded-md focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-foreground focus-visible:ring-offset-2 focus-visible:ring-offset-background active:scale-98">
                <div>
                    X
                    <span class="sr-only">Close</span>
                </div>
            </Dialog.Close>
        </Dialog.Content>
    </Dialog.Portal>
</Dialog.Root>