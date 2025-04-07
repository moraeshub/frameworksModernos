<template>
  <v-card-title class="text-h5"> Lista de salas </v-card-title>

  <v-card-text>
    <v-btn
      color="primary"
      class="mb-4"
      @click="handleOpenAddRoom"
    >
      Novo Usuário
    </v-btn>

    <v-data-table
      :headers="headers"
      :items="rooms"
      item-value="id"
    >
      <template #item.actions="{ item }">
				<v-btn icon color="primary" @click="handleOpenEditRoom(item)">
					<v-icon>mdi-pencil</v-icon>
				</v-btn>

				<v-btn icon color="red" @click="deleteUser(item.id)" class="ml-2">
					<v-icon>mdi-delete</v-icon>
				</v-btn>
			</template>
		</v-data-table>
	</v-card-text>

	<AddRoom v-model="showAddRoom" :room="room" @save="handleSaveAddRoom" />

	<EditRoom v-model="showEditRoom" :room="room" @save="handleSaveEditRoom" />
</template>

<script setup lang="ts">
import { ref } from "vue";

interface Room {
	id: number;
	room: string;
	teacher: string;
	status: string;
}
const showAddRoom = ref(false);
const showEditRoom = ref(false);

const emptyRoom = ref<Room>({
	id: 0,
	room: "",
	teacher: "",
	status: "",
});

const room = ref({ ...emptyRoom.value });

const headers = [
	{ title: "ID", key: "id", align: "start" },
	{ title: "Sala", key: "room", align: "start" },
	{ title: "Professor", key: "teacher", align: "start" },
	{ title: "Status", key: "status", align: "start" },
	{ title: "Ações", key: "actions", align: "end", sortable: false },
];

const rooms = ref<Room[]>([
	{ id: 1, room: "D-12", teacher: "joao@email.com", status: "ocupado" },
	{ id: 2, room: "O-8", teacher: "maria@email.com", status: "ocupado" },
]);

const handleOpenAddRoom = () => {
	showAddRoom.value = true;
};

const handleSaveAddRoom = (data: Room) => {
	const id = rooms.value.length + 1;
	rooms.value.push({
		id,
		room: data.room,
		teacher: data.teacher,
		status: data.status
	});
	room.value = emptyRoom.value;
	showAddRoom.value = false;
};

const handleOpenEditRoom = (data: Room) => {
	room.value = data;
	showEditRoom.value = true;
};

const handleSaveEditRoom = (data: Room) => {
	if (data.id) {
		// Edição: substitui o item com mesmo ID
		const index = rooms.value.findIndex((r) => r.id === data.id);
		if (index !== -1) {
			rooms.value[index] = { ...data };
		}
	} else {
		// Criação: adiciona novo com ID novo
		const id = rooms.value.length + 1;
		rooms.value.push({
			id,
			room: data.room,
			teacher: data.teacher,
			status: data.status
		});
	}

	room.value = { ...emptyRoom.value };
	showEditRoom.value = false;
};

function deleteUser(id: number) {
	rooms.value = rooms.value.filter((user) => user.id !== id);
}
</script>
