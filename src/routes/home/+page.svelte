<script lang="ts">
    import {onMount} from "svelte";
    import '../../app.css';

    let posts = [
        {
            "post_id": "abcde",
            "content": "This is a post",
            "timestamp": "1727482798",
            "posterId": "12345",
            "username": "user1"
        },
        {
            "post_id": "abcde",
            "content": "This is a post2",
            "timestamp": "1727482798",
            "posterId": "12345",
            "username": "user1"
        },
        {
            "post_id": "abcde",
            "content": "This is a post3",
            "timestamp": "1727482798",
            "posterId": "12345",
            "username": "user1"
        }
    ];

    onMount(() => {
        //Call API
    });
</script>

<div class="flex justify-center">

</div>

