<template>
    <div id="webviewer" ref="viewer"></div>
</template>

<script>

import WebViewer from '@pdftron/webviewer'

export default {
    name: 'WebViewer',
    props: { initialDoc: { type: String }},
    
    mounted(){
        WebViewer(
      {
        path: `${process.env.BASE_URL}webviewer`,
        initialDoc: this.initialDoc
      },
      this.$refs.viewer
    ).then((instance) => {
        instance.setTheme("light")
        const { annotationManager } = instance.Core;
        
        annotationManager.addEventListener('deletReply', (annotation, root)=> {
          annotationManager.createAnnotationReply(root, `Comment was gaya by ${annotationManager.getCurrentUser()}`);
        })
    });
  }
}

</script>

<style scoped>

 #webviewer { 
     height: 800px;
 }
</style>