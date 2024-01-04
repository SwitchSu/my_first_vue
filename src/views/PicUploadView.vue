<script>
export default {
    data() {
        return {
            picFile: '',
            filePic: '',
            imgFile: [],
        }
    },
    methods: {
        uploadPic(event) {
            // console.log(event);
            this.picFile = event.target.files[0];
            console.log(this.picFile);
            if (this.picFile) {
                const reader = new FileReader();
                reader.readAsDataURL(this.picFile);
                reader.onload = (e) => {
                    console.log(e);
                    this.filePic = e.target.result;
                    this.imgFile = [{
                        name: this.picFile.name,
                        path: this.filePic,
                    }];
                }
            }
        },
        submit() {
            this.imgFile
        }
    }
}
</script>
<template>
    <img :src="filePic" alt="">
    <input type="file" accept=".png,.jpg" @change="uploadPic">
    <!-- <button type="button" @click="submit()">Upload</button> -->
</template>
<style scoped></style>