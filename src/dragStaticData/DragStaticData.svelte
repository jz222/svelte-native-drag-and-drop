<script>
    const dragStartHandler = (e) => {
        console.log('Drag started.');

        e.dataTransfer.setData('text/plain', 'This message comes from the dragged element.');
    };

    const dropHandler = (e) => {
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

        <div on:drop|preventDefault="{dropHandler}" on:dragover|preventDefault>
            Drop here
        </div>
    </div>

</section>