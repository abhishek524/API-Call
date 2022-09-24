<html>
    <body>
        <form onsubmit="saveToLocalStorage(event)">
            <label> Name</label>
            <input type="text" name="username"  required/>
            <label> EmailId</label>
            <input type="email" name="emailId"  required/>
            <label> Phone Number</label>
            <input type="tel" name="phonenumber" />
            <button> Submit </button>
        </form>
        <ul id='listOfUsers'></ul>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.27.2/axios.min.js "></script>
        <script>
            function saveToLocalStorage(event) {
                event.preventDefault();
                const name = event.target.username.value;
                const email = event.target.emailId.value;
                const phonenumber = event.target.phonenumber.value;
                // localStorage.setItem('name', name);
                // localStorage.setItem('email', email);
                // localStorage.setItem('phonenumber', phonenumber)
                const obj = {
                    name,
                    email,
                    phonenumber
                }
                axios.post("https://crudcrud.com/api/4f0538fffbcf419b8605b6f295261886/appointmentData", obj)
                .then((Response)=>
                {
                    console.log(Response)
                })
                .catch((err)=>
                {
                    console.log(err)
                })
                axios.get("https://crudcrud.com/api/4f0538fffbcf419b8605b6f295261886/appointmentData",obj)
                .then((Response)=>
                {
                    console.log(Response)
                })
                .catch((err)=>
                {
                    console.log(err)
                })
               
                // axios.delete("https://crudcrud.com/api/4f0538fffbcf419b8605b6f295261886/appointment", obj)
                // .then((Response)=>
                // {
                //     console.log(Response)
                // })
                // .catch((err)=>
                // {
                //     console.log(err)
                // })
                // localStorage.setItem(obj.email, JSON.stringify(obj))
                // showNewUserOnScreen(obj)
            }


            window.addEventListener("DOMContentLoaded", () => {
                axios.get("https://crudcrud.com/api/4f0538fffbcf419b8605b6f295261886/appointmentData")
                .then((Response)=>
                {
                    console.log(Response)
                    for(var i=0;i<Response.data.length;i++)
                    {
                        showNewUserOnScreen(Response.data[i])
                    }
                })
                .catch((err)=>
                {
                    console.log(err)
                })
                const localStorageObj = localStorage;
                const localstoragekeys  = Object.keys(localStorageObj)

                for(var i =0; i< localstoragekeys.length; i++){
                    const key = localstoragekeys[i]
                    const userDetailsString = localStorageObj[key];
                    const userDetailsObj = JSON.parse(userDetailsString);
                    showNewUserOnScreen(userDetailsObj)
                }
            })

            function showNewUserOnScreen(user){
                const parentNode = document.getElementById('listOfUsers');
                const childHTML = `<li id=${user.email}> ${user.name} - ${user.email}
                                        <button onclick=deleteUser('${user.email}')> Delete User </button>
                                     </li>`

                parentNode.innerHTML = parentNode.innerHTML + childHTML;
            }

            // deleteUser('abc@gmail.com')

            function deleteUser(emailId){
                console.log(emailId)
                localStorage.removeItem(emailId);
                removeUserFromScreen(emailId);

            }

            function removeUserFromScreen(emailId){
                const parentNode = document.getElementById('listOfUsers');
                const childNodeToBeDeleted = document.getElementById(emailId);

                parentNode.removeChild(childNodeToBeDeleted)
            }







        </script>


    </body>
</html>
