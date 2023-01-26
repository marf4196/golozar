<template>
    <!-- Modal -->
    <div class="modal fade" :id="target" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content px-2">
                <div class="modal-header">
                    <div class="d-flex align-items-center">
                        <img src="../assets/images/modal-icon.png">
                        <h5 class="modal-title ps-3" id="exampleModalLabel">{{modalTitle}}</h5>
                    </div>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body py-4">
                    {{modalBody}}
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        modalBody: Text,
        modalTitle: Text,
        target: Text
    }
}
</script>
<style>
    
</style>