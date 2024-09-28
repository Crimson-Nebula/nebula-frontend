<script lang="ts">
    import { Dialog } from "bits-ui";
    import {fade} from "svelte/transition";
    import '../app.css';
    import GoogleWrapper from "./GoogleWrapper.svelte";
</script>

<Dialog.Root>
    <Dialog.Trigger class="btn">
        Log In
    </Dialog.Trigger>
    <Dialog.Portal>
        <Dialog.Overlay
                transition={fade}
                transitionConfig={{ duration: 150 }}
                class="fixed inset-0 z-50 bg-black/80"
        />
        <Dialog.Content class="fixed prose left-[50%] top-[50%] z-50 translate-x-[-50%] translate-y-[-50%] modal-box">
            <Dialog.Title class="flex w-full items-center justify-center">
                <h1>Log In</h1>
            </Dialog.Title>
            <div class="flex justify-center">
                <GoogleWrapper/>
            </div>
            <Dialog.Close class="absolute right-5 top-5 rounded-md focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-foreground focus-visible:ring-offset-2 focus-visible:ring-offset-background active:scale-98">
                <div>
                    X
                    <span class="sr-only">Close</span>
                </div>
            </Dialog.Close>
        </Dialog.Content>
    </Dialog.Portal>
</Dialog.Root>

<svelte:head>
    <script src="https://accounts.google.com/gsi/client" async></script>
</svelte:head>