<template>
    <main class="table">
        <table>
            <thead>
                <tr>
                    <td>
                        <button @click="sortBy('fname')">First Name</button>
                    </td>
                    
                    <td>
                        <button @click="sortBy('lname')">Last Name</button>
                    </td>
                    
                    <td>
                        <button @click="sortBy('gender')">Gender</button>
                    </td>
                    
                    <td>
                        <button @click="sortBy('job')">Job</button>
                    </td>
                </tr>
            </thead>

            <tbody>
                <tr v-for="row in alphabeticalSort">
                    <td v-for="value in row">{{ value }}</td>
                </tr>
            </tbody>
        </table>
    </main>
</template>

<script>
    const mockData = `[{"fname":"Issie","lname":"Phinnis","gender":"Agender","job":"Accountant I"}, {"fname":"Dyann","lname":"Corriea","gender":"Female","job":"Account Executive"}, {"fname":"Nicholle","lname":"Vallack","gender":"Genderqueer","job":"Research Assistant I"}, {"fname":"Drake","lname":"Cunliffe","gender":"Polygender","job":"Systems Administrator III"}, {"fname":"Bessy","lname":"Goodrum","gender":"Bigender","job":"Human Resources Manager"}, {"fname":"Sydelle","lname":"Duesberry","gender":"Bigender","job":"Programmer Analyst III"}, {"fname":"Crichton","lname":"Le Marchant","gender":"Genderfluid","job":"Editor"}, {"fname":"Aymer","lname":"Thorn","gender":"Genderfluid","job":"Speech Pathologist"}, {"fname":"Kelcie","lname":"Mcmanaman","gender":"Agender","job":"VP Marketing"}]`
	
    export default {
		data() {
			return {
                sort: {
                    key: 'fname',
                    order: 'asc'
                },

                content: JSON.parse(mockData)
            }
		},

        computed: {
            alphabeticalSort() {
                const key = this.sort.key;

                function sortFunction(a, b) {
                    if (a[key] > b[key]) {
                        return 1;
                    } else if (a[key] < b[key]) {
                        return -1;
                    } else {
                        return 0;
                    }
                }

                return this.content.sort(sortFunction)
            }
        },
        
        methods: {
            sortBy(key) {
                this.sort.key = key;
            }
        }
	}
</script>

<!-- 
    1 Lager en liste med objekter: mockData
    2 Tabellen er default sortert etter fname
    3 Parse lager verdien til mockData
    4 Verdiene blir sortert utifra bokstavenes index
    5 Deretter blir det returnert 
    6 Funksjonen sortBy aktiverer sorteringen
-->

<style>
    .table {
        width: 100vw;
    }

    table {
        margin-top: 50px;
        border-collapse: collapse;
        width: 80vw;
        margin-left: auto;
        margin-right: auto;
    }

    thead {
        font-weight: bold;
        font-size: 0.9em;
        width: 80vw;
    }

    table button:hover {
        color: rgba(0, 0, 0, 0.377);
    }

    table tbody {
        font-size: 0.8em;
        width: 80vw;
    }

    table tr {
        border: 1.5px solid black;
    }

    table td {
        padding: 0.5em 1em 0.5em 1em;
    }
</style>