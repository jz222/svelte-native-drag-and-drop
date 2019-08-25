<script>
    const dragStartHandler = (e) => {
        // Required to make it work in Firefox, but not
        // used in this example.
        e.dataTransfer.setData('text/plain', null);

        console.log('Drag started.');
    };

    const dragOverHandler = () => {
        console.log('Dragged element entered drop area.');
    };

    const dropHandler = () => {
        console.log('Dropped element in drop area.');

        alert('Element dropped in drop area.');
    };
</script>

<section>

    <h1>Simple Drag and Drop Event</h1>

    <div class="dndArea">
        <div>
            <div
                    class="draggableItem"
                    draggable="true"
                    on:dragstart="{dragStartHandler}"
            >
                Drag me!
            </div>
        </div>

        <div on:drop|preventDefault="{dropHandler}" on:dragover|preventDefault="{dragOverHandler}">
            Drop here
        </div>
    </div>

</section>