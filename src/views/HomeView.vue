<template>
  <main>
    <div id="retrievedTasky"></div>
    <div class="mx-auto mt-[100px] w-[90%] bg-gray-900 p-[20px] rounded-xl">
      <h1 class="text-white font-bold font-sans text-[25px]">Task List</h1>
      <form class="w-[100%] flex mt-[20px]" id="new-task-form">
        <input type="text" class="w-[70%] p-[10px] rounded-xl focus:outline-none" id="new-task-input" placeholder="Your Plans">
        <button type="submit" class="ml-[30px] bg-transparent text-indigo-500 font-bold text-[10px] md:text-[20px]" id="new-task-submit">Add Task</button>
      </form>
    </div>

    <section class="mt-[50px] p-[20px]">
      <h2 class="text-indigo-800 font-bold text-[25px]">Tasks</h2>

      <div id="tasks">

      </div>
    </section>
  </main>
</template>

<script>
  window.addEventListener("load", () => {
    const form = document.getElementById("new-task-form");
    const input = document.getElementById("new-task-input");
    const list_el = document.getElementById("tasks");

    var retrievedTasky = document.getElementById("retrievedTasky");
    retrievedTasky.innerText = "Last Retrieved: " + localStorage.getItem("Task");

    form.addEventListener('submit', (e) => {
      e.preventDefault();

      const task = input.value;

      if(!task) {
        alert("Please fill out the task");
        return;
      }

      const task_el = document.createElement("div");
      task_el.classList.add("task");

      const task_content_el = document.createElement("div");
      task_content_el.classList.add("content");
      task_content_el.innerText = task;
      task_content_el.style.display = "none";

      task_el.appendChild(task_content_el);
      const task_input_el = document.createElement("input");
      task_input_el.classList.add("text");
      task_input_el.type = "text";
      task_input_el.value = task;
      task_input_el.setAttribute("readonly", "readonly");
      task_el.appendChild(task_input_el);

      const task_action_el = document.createElement("div")
      task_action_el.classList.add("actions");

      const task_edit_el = document.createElement("button")
      task_edit_el.classList.add("edit");
      task_edit_el.innerHTML = "Edit";

      const task_delete_el = document.createElement("button")
      task_delete_el.classList.add("delete");
      task_delete_el.innerHTML = "Delete";

      task_action_el.appendChild(task_edit_el)
      task_action_el.appendChild(task_delete_el)

      task_el.appendChild(task_action_el)

      list_el.appendChild(task_el);

      input.value = "";

      localStorage.setItem("Task", JSON.stringify(task_input_el.value))
      var retrievedTask = localStorage.getItem("Task");
      console.log(retrievedTask);

      for(let i=0; i<localStorage.length; i++){
        console.log(localStorage);
      }

      task_edit_el.addEventListener("click", () => {
        if(task_edit_el.innerText.toLowerCase() == "edit") {
          task_input_el.focus();
          task_edit_el.innerText = "Save";
          task_input_el.removeAttribute("readonly");
          localStorage.setItem("Task", JSON.stringify(task_input_el.value))
        }
        else {
          // task_content_el.innerText = task_input_el.value
          task_edit_el.innerText = "Edit"
          task_input_el.setAttribute("readonly", "readonly");
          localStorage.removeItem("Task", JSON.stringify(task_input_el.value))
        }
      })

      task_delete_el.addEventListener("click", () => {
        list_el.removeChild(task_el);
      })
    })
  })
</script>

<style>
  .task {
    width: 100%;
    position:relative;
    background: #111827;
    color: white;
    padding: 20px;
    border-radius: 30px;
    margin-top: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .content {
    padding: 10px;
  }
  .actions {
    font-size: 16px;
    padding:10px;
    display: flex;
  }
  .edit {
    background: white;
    padding: 8px;
    color: #000;
    margin-right: 20px;
    border-radius: 10px;
  }
  .delete {
    background: red;
    padding: 8px;
    color: #fff;
    border-radius: 10px;
  }
  .text{
    color: black;
    background: transparent;
    color: white;
    justify-content: space-between;
    border: 0px;
    width:70%;
  }
  .text:focus {
    outline:none;
  }

  @media only screen and (max-width:767px) {
    .actions {
      font-size: 12px;
      padding:10px;
      display: flex;
    }
    .edit {
      background: white;
      padding: 8px;
      color: #000;
      margin-right: 5px;
      border-radius: 10px;
    }
    .delete {
      background: red;
      padding: 8px;
      color: #fff;
      border-radius: 10px;
    }
  }
</style>