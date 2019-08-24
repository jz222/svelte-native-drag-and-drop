<script>
    const dragStartHandler = (e) => {
        console.log('Drag started.');

        e.dataTransfer.setData('text/plain', 'This message comes from the dragged element.');
    };

    const dragOverHandler = (e) => {
        e.preventDefault();
    };

    const dropHandler = (e) => {
        e.preventDefault();
        console.log('Dropped element in drop area.');

        const data = e.dataTransfer.getData('text/plain');

        alert(data);
    };
</script>

<section>

    <h1>Drag Static Data</h1>

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

        <div on:drop="{dropHandler}" on:dragover="{dragOverHandler}">
            Drop here
        </div>
    </div>

</section>