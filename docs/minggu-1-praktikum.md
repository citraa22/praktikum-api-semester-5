maria citra/202434001/manajemen web servis









praktikum 1 - audit API dengan postman



**checkpoint 1 - request berhasil**



1. request
* method : GET
* endpoint : /users/octocat
* URL : https://api.github.com/users/octocat



2\. header

* accept : application/vnd.github+json
* X-Github-Api-Version: 2022-11-28



3\. response

* status code: 200 OK
* logn: octocat
* ID: 583231
* public repositories: 8
* URL: https://api.github.com/users/octocat





**checkpoint 2 - request gagal**



1. request
* method : GET
* endpoint: https://api.github.com/users/user-tidak-ada-987654321



2\. hasil 

* status code: 404 not found



3\. perbandingan

* Yang berubah pada  usernamenya, request yang pertama itu pakai octocat sedangkan yang kedua pakai username yang tidak ada
* Status yang awalnya 200 OK menjadi 404 not found
* Jika gagal bisa tau karena ada kode 404 not found
* Karena respone yang gagal juga ada bodynya, jadi adanya body belum tentu request berhasil. 





**kesimpulan** 

API GitHub menggunakan method GET untuk memngambil data pengguna. client mengirim request ke endpoint GitHub rest API dan menerima response dalam bentuk json. status code membantu mengetahui request berhasil atau gagal  



