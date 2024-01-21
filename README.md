ap;
  align-items: center;
  justify-content: center;
}

.main {
  font-family: "Baloo Bhai 2", sans-serif;
  font-family: "Baloo Bhaijaan 2", sans-serif;
  font-family: "Poppins" {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#repo-div {
  margin: 30px 0;
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wr, sans-serif;
  width: 100vw;
  height: auto;
}

.user-div {
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 40%;
  width: 100%;
  padding: 0 0 0 3%;
}

.left {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.right {
  /* margin: 0 10px; */
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* padding-top: 20px; */
}

img {
  height: 200px;
  width: 200px;
  border-radius: 50%;
}

/* .right p {
    margin: 5px 0;
}

.right h1 {
    margin: 5px 0;
} */

.link {
  padding: 10px 0;
  font-weight: bold;
}

.content {
  padding-left: 10px;
  margin: 10px 20px 10 0;
  position: absolute;
  border: 2px solid black;
  border-radius: 50px;
  height: 30px;
}

.content input {
  height: 100%;
  border: none;
  outline: none;
  font-size: 17px;
  padding: 0 5px;
  border-radius: 50px;
}

.search-div {
  display: flex;
  flex-direction: row;
  justify-content: end;
  align-items: center;
  margin: 30px 0;
  padding-right: 50px;
  height: 20%;
  width: 100%;
}

.right p a {
  color: black;
}

.right p a:hover {
  color: red;
}

.left a:hover {
  color: red;
}

.left a {
  color: black;
}

.ri-twitter-fill {
  font-size: 20px;
  color: #1da1f2;
  font-weight: bold;
}

.ri-github-fill {
  font-size: 20px;
  font-weight: bold;
}

.links {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.links a {
  padding-left: 5px;
}

et userApi = fetch("https://api.github.com/users/hiteshchoudhary");
let SearchInput = document.getElementById("search");

userApi.then((value) => {
    return value.json();
}).then((data) => {
    document.getElementById('user-name').innerHTML = data.name;
    document.getElementById('bio').innerHTML = data.bio;
    document.getElementById('location').innerHTML = data.location;
    document.getElementById('github').innerHTML = data.html_url;
    document.getElementById('twitter').innerHTML = data.twitter_username;
    document.getElementById('user-img').setAttribute("src", data.avatar_url)
}).catch(error => console.log(error))

async function getRepo() {
    let userRepo = await fetch("https://api.github.com/users/hiteshchoudhary/repos");

    const RepoJson = await userRepo.json();
    return RepoJson;
}
async function displayRepo() {
    let data = await getRepo();

    const style1 = "width:400px; height:210px; border-width:2px; border-color:black; border-radius:10px; border-style:solid; margin:15px; display:flex; flex-direction:column; align-items:center; justify-content:flex-start; cursor:pointer;";

    const style2 = "font-size:13px; font-weight:normal; border:1px solid black; border-radius:50px; width:50px; display:flex; justify-content:center; align-items:center; height:20px; margin: 0 3px";

    let RepoPara = document.getElementById("repo-div");
    for (let dt of data) {
        let myLink = document.createElement('a');
        myLink.setAttribute("href", dt.html_url)
        myLink.setAttribute("target", "_blank")
        myLink.style = "text-decoration:none; color:black; cursor:auto;";

        let box = document.createElement('div');
        box.style = style1;
        let heading = document.createElement("h3");
        heading.style = "margin-top:5px; display:flex; flex-direction:row; align-items:center;"
        let para = document.createElement("p");
        para.style = "padding:10px; font-size:15px"
        para.textContent = dt.description
        let span = document.createElement('span')
        span.textContent = " Public"
        span.style = style2
        heading.textContent = `${dt.name}`
        let span1 = document.createElement("span");
        span1.textContent = `🟣${dt.language} | `
        let span2 = document.createElement("span");
        span2.textContent = `⭐${dt.stargazers_count} | `
        let span3 = document.createElement("span");
        span3.textContent = ` 🇬🇮 ${dt.forks_count}`
        let lastpara = document.createElement("p");


        heading.appendChild(span)
        box.appendChild(heading)
        box.appendChild(para)
        box.appendChild(lastpara)
        myLink.appendChild(box)
        RepoPara.appendChild(myLink)
        lastpara.appendChild(span1)
        lastpara.appendChild(span2)
        lastpara.appendChild(span3)
    }
}
displayRepo();
