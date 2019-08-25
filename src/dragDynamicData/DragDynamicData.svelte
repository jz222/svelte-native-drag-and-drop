<script>
    let droppedUser;

    const dragStartHandler = (e, id) => e.dataTransfer.setData('text/plain', id);

    const dropHandler = (e) => {
        const userId = e.dataTransfer.getData('text/plain');
        droppedUser = users.find(x => x.id === +userId);
    };

    const users = [
        { id: 1, firstName: 'John', lastName: 'Doe', email: 'jd@example.com', age: 40 },
        { id: 2, firstName: 'Kathrin', lastName: 'Smith', email: 'ks@example.com', age: 28 },
        { id: 3, firstName: 'Max', lastName: 'Hammer', email: 'mh@example.com', age: 22 },
        { id: 4, firstName: 'Anna', lastName: 'Riley', email: 'ar@example.com', age: 25 }
    ];
</script>

<section>

    <h1>Drag Dynamic Data</h1>

    <div class="dndArea">
        <div>
            {#each users as user}
                <div
                        class="draggableItem"
                        draggable="true"
                        on:dragstart="{(e) => dragStartHandler(e, user.id)}"
                >
                    {user.firstName}
                </div>
            {/each}
        </div>

        <div on:drop|preventDefault="{dropHandler}" on:dragover|preventDefault>
            {#if droppedUser}
                <ul>
                    <li><b>First Name:</b> {droppedUser.firstName || 'Not available'}</li>
                    <li><b>Last Name:</b> {droppedUser.lastName || 'Not available'}</li>
                    <li><b>Email:</b> {droppedUser.email || 'Not available'}</li>
                    <li><b>Age:</b> {droppedUser.age || 'Not available'}</li>
                </ul>
            {:else}
                Drop here
            {/if}
        </div>
    </div>

</section>
