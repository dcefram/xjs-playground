## XJS Test App

I'm currently doing some experimental work for XJS Framework 3.0, and this is what I use to actually
test it out manually.

Pre-req: npm link the local xjs directory.

```
# first, install all of the dependencies (ie. svelte stuff)
npm i

# in xjs 3.0 directory
npm link

# in xjs-playground directory
npm link xjs

# now we can run the test app!
npm run dev
```

Some coolkid gif

![Item Shuffler](xjs-test-app-1.gif "Simple item shuffling")