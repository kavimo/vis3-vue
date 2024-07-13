# vis3-vue
Kavimo Vis3 Vue Component

# Installation:
```
npm i @kavimo/vis3-vue
```

# Use in Nextjs Home:
```
<script setup>
import Vis3 from '@kavimo/vis3-vue';

const handleLoad = ( media ) => {
    console.log('Vis: Media Loaded');
    console.log( media )
}
</script>

<template>
  <main>
    <Vis3 :onLoad=handleLoad domainName="stream.domain.com" ID="xxxxxxxxxxxx" />
  </main>
</template>

```