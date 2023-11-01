# NoteAppxCloudRun
Ini adalah repository pendeployan note app menggunakan cloud run (back-end)

Notes API merupakan backend (dari Notes App) yang akan kita deploy terlebih dahulu. Notes API akan kita deploy menggunakan metode deployment via container image.

## Langkah pertama yang harus kita lakukan adalah clone source code Notes API dari GitHub repository milik Dicoding
## Klik Activate Cloud Shell yang berada di pojok kanan atas halaman
 <a href="#"><img align="center" alt="GCP" title="GCP" width="620px" src="https://storage.googleapis.com/malesbanget/ss.png" /></a>  
## Pada shell prompt, jalankan perintah berikut ini untuk melakukan clone
```cmd 
git clone -b notes-api https://github.com/dicodingacademy/a133-gcp-labs.git notes-api
```

## Pindah ke directory notes-api (hasil dari proses clone barusan)
```cmd
cd notes-api/
```
## Buat berkas baru bernama *Dockerfile*
```cmd
nano Dockerfile
```
## Salin baris kode berikut ini ke berkas *Dockerfile*
```cmd
FROM node:14.21.2-alpine
WORKDIR /app
ENV PORT 5000
COPY . .
RUN npm install
EXPOSE 5000
CMD [ "npm", "run", "start"]
```
Jangan lupa simpan berkas Dockerfile dengan **CTRL+X** -> **Y** -> **Enter**.

##  Lanjut kita buat sebuah container image baru dari berkas Dockerfile tersebut menggunakan Cloud Build
```cmd
gcloud builds submit --tag gcr.io/<project-id>/backend
```
Ganti <project-id> dengan Project ID Anda. Project ID tertulis di sebelah shell prompt.

## Container image kita sudah sukses tersimpan di Container Registry. Sekarang kita sudah bisa deploy Notes API ke Cloud Run. Silakan gunakan perintah ini
```cmd
gcloud run deploy --image gcr.io/<project-id>/backend
```
## Setelah deployment berhasil, Anda akan menerima Service URL. Buka tautan tersebut dan pastikan menampilkan hasil sebagai berikut.
```{"statusCode":404,"error":"Not Found","message":"Not Found"}```
