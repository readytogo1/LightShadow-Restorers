<template>
    <div class="image-container" ref="container" @wheel="handleWheel">
        <img :src="imageUrl" :style="{ transform: `scale(${scale})` }" @load="updateImageSize">
    </div>
</template>
    
<script>
export default {
    props: {
        imageUrl: {
            type: String,
            required: true,
        },
        scale: {
            type: Number,
            required: true,
        },
    },
    methods: {
        updateImageSize() {
            const image = new Image();
            image.src = this.imageUrl;
            image.onload = () => {
                this.$emit('update:imageSize', {
                    width: image.width,
                    height: image.height,
                });
            };
        },
        handleWheel(event) {
            if (event.ctrlKey) {
                event.preventDefault();

                const delta = -Math.sign(event.deltaY);
                const newScale = this.scale + delta * 0.1;

                // 控制缩放比例在 0.1 到 2.5 之间
                const clampedScale = Math.max(Math.min(newScale, 2.5), 0.1);

                this.$emit('update:scale', clampedScale);
            }
        },

    },
};
</script>
    
<style>
.image-container {
    width: 500px;
    height: 500px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
}

.image-container img {
    user-select: none;
}
</style>
    