<template>
    <div className="container">
        <table className="table table-hover">
            <thead className="thead-light">
            <tr>
                <th scope="col">#</th>
                <th scope="col">Title</th>
                <th scope="col">Content</th>
                <th scope="col">Person In Charge</th>
                <th scope="col">Show</th>
                <th scope="col">Edit</th>
                <th scope="col">Delete</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="task in tasks">
                <th scope="row">{{ task.id }}</th>
                <td>{{ task.title }}</td>
                <td>{{ task.content }}</td>
                <td>{{ task.person_in_charge }}</td>
                <td>
                    <router-link v-bind:to="{name: 'task.show', params: {taskId: task.id }}">
                        <button className="btn btn-primary">Show</button>
                    </router-link>
                </td>
                <td>
                    <router-link v-bind:to="{name: 'task.edit', params: {taskId: task.id }}">
                        <button className="btn btn-success">Edit</button>
                    </router-link>
                </td>
                <td>
                    <button className="btn btn-danger">Delete</button>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            tasks: []
        }
    },
    methods: {
        getTasks() {
            axios.get('/api/tasks')
                .then((res) => {
                    this.tasks = res.data;
                });
        }
    },
    mounted() {
        this.getTasks();
    }
}
</script>
