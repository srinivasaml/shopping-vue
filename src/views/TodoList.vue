<!DOCTYPE html>

<html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap" rel="stylesheet">
        <link rel="stylesheet" href="style.css">
        <title>To-Do List</title>
    </head>

    <body>
        
        <main id="app">
            
            <section class="todo-list">
                
                
                <h3>To-do List</h3>
                
                <div class="all-todos">
                    <div 
                        class="single-todo" 
                        v-for="todo in todos"
                        :class="{done : todo.done}"
                        @click="todo.done = !todo.done">
                        <p>{{todo.text}}</p>
                    </div>
                </div>

                <button v-if="todos.length" class="clear" @click="todos=[]">Clear All</button>

                <input type="text" placeholder="Add new to-do" v-model="newTodo.text">
                <button class="add" @click="addTodo()">Add</button>

                <div class="instructions">
                    Instructions:
                    <ul>
                        <li>Click the to-do text to toggle between done / undone</li>
                        <li>Use clear all button to remove all items</li>
                        <li>Use the input field to add new to-dos</li>
                    </ul>
                </div>
            </section>

        </main>
        <script src="https://unpkg.com/vue@next"></script>
        <script >
        
const todosApp = {
    data() {
        return {
            todos: [],
            newTodo: {
                done: false
            }
        }
    },
    methods: {
        addTodo: function() {
            if (this.newTodo.text) {
                this.todos.push(this.newTodo);
                this.newTodo = {
                    done: false
                };
                localStorage.setItem("todos", JSON.stringify(this.todos));
            } else {
                alert("To-do text is required");
            }
        }
    },
    created() {
        this.todos = localStorage.getItem("todos") ? JSON.parse(localStorage.getItem("todos")) : this.todos;
    },
    updated() {
        localStorage.setItem("todos", JSON.stringify(this.todos));
    }

}

Vue.createApp(todosApp).mount('#app');
        </script>
    </body>

<style>
body {
    margin: 0;
    font-family: 'Open Sans', sans-serif;
}

main {
    display: flex;
    justify-content: center;
    align-items:flex-start;
    flex-wrap: wrap;
    padding-top: 60px;
}

main .todo-list input {
    box-sizing: border-box;
    height: 28px;
    border-radius: .25rem;
    width: 80%;
    border: 1px solid lightgrey;
    margin-top: 32px;
}

main button {
    background-color: transparent;
    cursor: pointer;
    box-sizing: border-box;
    height: 28px;
    border-radius: .25rem;
    color: #fff;
}

main button:hover {
    opacity: 0.8;
}

main button.add {
    background-color: #007bff;
    border: 1px solid  #007bff;
    margin-left: 2px;
}

main button.clear {
    background-color: #dc3545;
    border: 1px solid #dc3545;
    display: block;
    margin: auto;
}

main button:focus {
    outline:0;
}

main > section.todo-list h3 {
    text-align: center;
    margin-top: 24px;
    width: 100%;
}


main > section.todo-list {

    flex-wrap: wrap;
    border: 1px solid lightgrey;
    background-color: rgb(248, 248, 248);
    padding: 20px;
    max-width: 500px;
    min-width: 300px;
    text-align: center;
    border-radius: .25rem;
}

main .all-todos .single-todo {
    display: flex;
    align-items: center;
    justify-content: center;
    
}

main .all-todos .single-todo p {
    margin: 12px 0;
    cursor: pointer;
}

main .all-todos .single-todo.done p {
    text-decoration: line-through;
}

main .all-todos .single-todo button.remove {
    width: 12px;
    height: 12px;
    border: none;
    background: transparent url('img/remove.png') no-repeat center;
    background-size: contain;
    cursor: pointer;
    margin-left: 8px;
}

main > section.todo-list button.clear {

    margin-top: 24px;
}

div.instructions {
    font-size: 11px;
    margin-top: 40px;
    color: grey;
}

div.instructions ul {
    list-style: inside;
    text-align: center;
    padding: 0;
}

div.instructions ul li {
    margin: 4px auto;
}

</style>
</html>