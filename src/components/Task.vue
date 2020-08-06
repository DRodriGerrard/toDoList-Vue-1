<template>
    <div class="task">
        <div class="row">
            <div class="col-sm">
                <form class="form-group">
                    <input type="text" class="form-control input" :placeholder="task.title">
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Task',
    props: [
        'task'
    ]
}
</script>

<style lang="sass">
.task
    text-align: center
</style>