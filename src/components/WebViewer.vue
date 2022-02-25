<template>
    <div id="webviewer" ref="viewer"></div>
</template>

<script>

import WebViewer from '@pdftron/webviewer'

export default {
    name: 'WebViewer',
    props: { initialDoc: { type: String }},

    data() {
    return {
      annotations: [
        { page: 2, x: 150, y: 150, w: 50, h: 20, id: "1" },
        { page: 1, x: 80, y: 90, w: 50, h: 20, id: "2" },
        { page: 1, x: 120, y: 120, w: 50, h: 20, id: "3" },
      ],
    };
  },
    
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