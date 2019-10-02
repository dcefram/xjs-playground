<script>
  import Xjs from "xjs-framework";
  import ItemProps from "xjs-framework/dist/props/item-props";
  export let name;

  const xjs = new Xjs();

  function asyncReduce(stack, fn, def) {
    return stack.reduce(
      (promise, item, index) =>
        promise.then(previous => fn(previous, item, index)),
      Promise.resolve(def)
    );
  }

  async function handleClick() {
    const currentScene = await xjs.getView(0).getCurrentScene();
    const items = await currentScene.getItems();

    console.log(items);

    // Get their positions
    const positions = await asyncReduce(
      items,
      async (stack, item) => {
        const pos = await item.getProperty(ItemProps.position);

        return [...stack, pos];
      },
      []
    );

    // Now assign their positions randomly
    for (let cnt = 0; cnt < items.length; cnt++) {
      const idx = Math.floor(Math.random() * positions.length);
      const position = positions.splice(idx, 1);
      items[cnt].setProperty(ItemProps.position, position[0]);
    }
  }
</script>

<style>
  :global(body) {
    background-color: #eee;
  }

  h4 {
    color: #555;
    font-weight: normal;
  }
</style>

<h1>XJS 3.0 Playground</h1>

<h4>This test app can shuffle items in the current scene!</h4>

<button on:click={handleClick}>Shuffle items!</button>
