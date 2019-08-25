<script>
    let movedUsers = [];

    function dragStartHandler(e) {
        const userId = this.attributes.getNamedItem('data-userid').value;
        e.dataTransfer.setData('text/plain', userId);

        this.classList.add('draggedItem');

        setTimeout(() => this.className = 'hiddenItem', 1);
    }

    function dragEndHandler() {
        this.className = 'draggableItem';
    }

    const dropHandler = (e) => {
        const userId = e.dataTransfer.getData('text/plain');

        const user = users.find(u => u.id === +userId);

        if (!user) return;

        movedUsers = [...movedUsers, user];
        users = users.filter(u => u.id !== +userId);
    };

    let users = [
        { id: 1, firstName: 'John', lastName: 'Doe', email: 'jd@example.com', age: 40 },
        { id: 2, firstName: 'Kathrin', lastName: 'Smith', email: 'ks@example.com', age: 28 },
        { id: 3, firstName: 'Max', lastName: 'Hammer', email: 'mh@example.com', age: 22 },
        { id: 4, firstName: 'Anna', lastName: 'Riley', email: 'ar@example.com', age: 25 }
    ];
</script>

<section>

    <h1>Move Element</h1>

    <div class="dndArea">
        <div>
            {#each users as user}
                <div
                        class="draggableItem"
                        draggable="true"
                        data-userid="{user.id}"
                        on:dragstart="{dragStartHandler}"
                        on:dragend="{dragEndHandler}"
                >
                    {user.firstName}
                </div>
            {/each}
        </div>

        <div on:drop|preventDefault="{dropHandler}" on:dragover|preventDefault>
            {#if movedUsers.length}
                {#each movedUsers as user}
                    <div class="droppedItem">
                        {user.firstName}
                    </div>
                {/each}
            {:else}
                Drop here
            {/if}
        </div>
    </div>

</section>