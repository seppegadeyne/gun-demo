<script>
    import { onMount } from 'svelte'

    let hello


    // Initialize gun.
    // [localStorage] We are turning localStorage to false for testing purposes. Generally, you'd want that to be true
    // [secret] Secret should be something long and secure. Your data will be saved to Skynet using that secret
    // [portal] Skynet portal you'd like to use. Use a portal you trust or run your own. They could potentially manipulate your data (although I don't see why)
    // [debug] Show debug output
    // [until] Change the batch time of Gun so that it doesn't attempt to write to storage too quickly
    onMount(() => {
        window.gun = new Gun({
            localStorage: false,
            secret: "TopGeheimSecretWord",
            portal: "https://siasky.net",
            debug: false,
            until: 2*1000
        })

        // Put data into gun. This will store in memory, peers, then localStorage (disabled), then Skynet
        /* gun.get('hello').put(
            {
                name: "Seppe"
            }
        ); */

        // Get data into gun. This will pull from memory, peers, then localStorage (disabled), then Skynet
        gun.get('hello').on(data => {
            hello = data['name']
            console.log("hello: " + hello)
        })
    })

</script>

<svelte:head>
    <script src="https://cdn.jsdelivr.net/npm/gun/gun.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gun/lib/radix.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gun/lib/radisk.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gun/lib/store.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gun/lib/rindexed.js"></script>
    <script src="https://unpkg.com/zenbase/dist/main.js"></script>
</svelte:head>

GUN LOADED