# Upload File Gambar

## Instruksi Praktikum

1. Persiapkan text editor misalnya VSCode.
2. Buka kembali folder dengan nama lab11_ci pada docroot webserver (htdocs)
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.

## Langkah-langkah Praktikum

### 1. Upload Gambar pada Artikel

Menambahkan fungsi unggah gambar pada tambah artikel. Buka kembali Controller Artikel pada project sebelumnya, sesuaikan kode pada method add seperti berikut:

```PHP
public function add()
{
    // Validasi data.
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid)
    {
        $file = $this->request->getFile('gambar');

        // Pindahkan file gambar ke direktori yang ditentukan.
        $file->move(ROOTPATH . 'public/gambar');

        $artikel = new ArtikelModel();
        $artikel->insert([
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
            'slug' => url_title($this->request->getPost('judul')),
            'gambar' => $file->getName(),
        ]);

        return redirect('admin/artikel');
    }

    $title = "Tambah Artikel";
    return view('artikel/form_add', compact('title'));
}
```

2. Kemudian pada file views/artikel/form_add.php tambahkan field input file seperti berikut.

```php
<p>
    <input type="file" name="gambar">
</p>
```

3. Dan sesuaikan tag form dengan menambahkan ecrypt type seperti berikut.

```php
<form action="" method="post" enctype="multipart/form-data">
```

4. Ujicoba file upload dengan mengakses menu tambah artikel. http://localhost:8080/admin/artikel/add

![images-0](https://github.com/liskaniaaprilia/Program5Web/assets/115616044/32874641-7d4e-4523-9410-0541934db226)

5. Kemudian tambahkan judul artikel, keterangan artikel, serta tambahkan gambar artikel

![images-1](https://github.com/liskaniaaprilia/Program5Web/assets/115616044/9f9f53d9-2539-41d3-8554-2a74f03f1333)

6. Periksa apakah Artikel sudah masuk kedalam daftar artikel

![images-2](https://github.com/liskaniaaprilia/Program5Web/assets/115616044/8d22c3fd-34e9-435f-b2af-ebe8d4b207bb)

7. Tampilan hasil dari keseluruhan artikel

![images-3](https://github.com/liskaniaaprilia/Program5Web/assets/115616044/50d86ba2-ede2-4ebe-9633-0cd4057282f0)

# FINISH
