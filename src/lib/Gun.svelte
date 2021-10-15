<script>
    import Gun from 'gun'

    const gun = Gun({
        peers: [
            'https://gun.straffesites.com/gun'
        ]
    })

    let
        name = 'Hello',
        lastname = 'World',
        text

    function save(name, lastname) {
        gun.get('store').put(
            {
                name: name,
                lastname: lastname
            }
        )
    }

    gun.get('store').on(data => {
        console.log("data changed or loaded: " + JSON.stringify(data))
        text = JSON.stringify(data)
        name = data.name
        lastname = data.lastname
    })

    $: save(name, lastname)
</script>

<h1>GUN example</h1>
Name: <input bind:value={name} type="text">
Lastname: <input bind:value={lastname} type="text" style="margin-bottom:2rem;">

<div style="padding:2rem; background-color:lightgreen; margin-bottom: 2rem;">
    {text}
</div>

<div style="padding:2rem; background-color:lightblue;">
    Have a look at the console; when database gets updated it pushes data to the client.
</div>