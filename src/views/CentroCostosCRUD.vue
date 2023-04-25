<template>
    
    <div class="container">

    <div class="creation_bar"> 
        <form>
            <input name = "name" type="text" [(ngModel)]="userForm.name" placeholder="nombre" style="margin-right: 10px;">
            <input name = "email" type="text" [(ngModel)]="userForm.email" placeholder="email" style="margin-right: 10px;">
            <input name = "contraseña" type="text" [(ngModel)]="userForm.password" placeholder="password" style="margin-right: 10px;">
            <button (click)="addUser()">Agregar</button>
        </form>
    </div>

    <div class="table">
        <table>
            <tr>
            <th style="margin-right: 15px;">Codigo</th>
            <th style="margin-right: 10px;">Nombre Centro Costos</th>
            </tr>
            <tr *ngFor="let user of users">
            <td>{{ CentroCostos.codigo }}</td>
            <td>
                <span *ngIf="!user.editing" style="margin-right: 10px;">{{ CentroCostos.name }}</span>
                <input *ngIf="user.editing" style="margin-right: 10px;" type="text" [(ngModel)]="user.name">
            </td>
            <td>
                <button *ngIf="!user.editing" (click)="user.editing = true" style="margin-right: 10px;">Editar</button>
                <button *ngIf="user.editing" (click)="editUser(user.id, user.name, user.email, user.password); user.editing = false" style="margin-right: 10px;">Guardar</button>
                <button (click)="deleteUser(user.id)" style="margin-right: 10px;">Eliminar</button>
            </td>
            </tr>
        </table>
    </div>
    </div>
    <!-- <div>
        <ul class="list-group">
            <h1 > LISTA DE TAREAS</h1>
            <li
                class="list-group-item list-group-item-action p-4"
                style="cursor: pointer"
                v-for="(task, index) in tasks"
                :key="index"
                @click="this.$router.push(`/task/${task._id}`)"
            >
                {{ task.title }}
            </li>
        </ul>
  </div> -->
</template>

<script lang="js">
    // import { defineComponent } from "vue";
    // import { Cliente } from "../interfaces/cliente";

    // export default defineComponent ({
    //     name: "Clientes",
    //     data(){
    //         return {
    //             Codigo: "",
    //             NombreCentroCostos: ""
    //         };
    //     },
    //     methods: {

    //     }
    // });

        
    // users = [
    // { id: 1, name: 'Erick', email: 'erick@example.com',password: "12345", editing: false },
    // { id: 2, name: 'Lisette', email: 'lila@example.com',password: "54321", editing: false },
    // { id: 3, name: 'Martin', email: 'martin@example.com',password: "qwer", editing: false },
    // { id: 4, name: 'Nestor', email: 'nestor@example.com',password: "asdf", editing: false },
    // { id: 5, name: 'Diana', email: 'diana@example.com',password: "zxcv", editing: false },
    // ];


    // userForm = {
    //     id: 0,
    //     name: '',
    //     email: '',
    //     password: '',
    //     editing: false
    // }

    // nextId = 6;
    
    // addUser(); {
    //     this.userForm.id = this.nextId++;
    //     this.users.push({...this.userForm});
    //     this.userForm = {id: 0,name: '',email: '',password: '',editing: false};
    //     this.changeDetector.detectChanges();
    // }
                
    // deleteUser( id: number) {
    //     this.users = this.users.filter(user => user.id !== id);
    // }

    // editUser(id: number, name: string, email: string, password: string) {
    //     const user = this.users.find(user => user.id === id);
    //     if (user) {
    //     user.name = name;
    //     user.email = email;
    //     user.password = password;
    //     }
    // }

    // getUsers() {
    //     return this.users;
    // }
</script>

<style>

</style>
