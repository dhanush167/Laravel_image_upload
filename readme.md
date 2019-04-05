<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## 5.8 Laravel test only


Config folder->database.php
.env file check for database

1)php artisan make:migration create_sample_data_table--create=sample_data

2)database foler->migrations foler

3)php artisan migrate

4)php artisan make: model Crud-m

   go to app folder for->Crud.php
5)php artisan make:controller CrudsController --resource

go to App foler->Http foler->CrudsController.php


 $data=Crud::latest()->paginate(5);
return view('index',compact('data'))->with('i',(request()->input('page',1)-1)*5);

<h2>





<h1>image cropping</h1>

<h3>

A few days ago i was working on my php laravel 5.8 new project. i exactly remember i was working on user profile page and i need to add image upload on my user profile page. but i know image uploading is simple with laravel 5.6, but i also need to add crop and preview image before save image in folder.

I was thinking how can i do it easily, i decide to do with my own jquery but after write some code. i thought it will take time and need to write large amount of code. but after some time, finally decide to use any one jquery plugin i can done crop image and also show preview of profile image. After google search i found Croppie plugin. so i checked website of Croppie plugin and i done to with it

</h3>


<h4>https://hdtuto.com/article/laravel-56-preview-and-crop-image-before-upload-using-ajax</h4>

<h3>Step 1: Create Routes In web.php</h3>

<p>Route::get('crop-image', 'ImageController@index');</p>

<p>Route::post('crop-image', ['as'=>'upload.image','uses'=>'ImageController@uploadImage']);</p>


<h3>
    Step 2: Create ImageController Controller
</h3>

<p>
    <?php



namespace App\Http\Controllers;



use Illuminate\Http\Request;



class ImageController extends Controller

{



    public function index()

    {

      return view('imageUpload');

    }



    public function uploadImage(Request $request)

    {

        $image = $request->image;



    list($type, $image) = explode(';', $image);

    list(, $image)      = explode(',', $image);

    $image = base64_decode($image);

    $image_name= time().'.png';

    $path = public_path('upload/'.$image_name);



    file_put_contents($path, $image);

    return response()->json(['status'=>true]);

    }

    }
</p>

<h3>Step 3: Create imageUpload.blade.php Blade</h3>

<p>

    <html lang="en">

    <head>

        <title>Laravel 5.6 - Preview and Crop Image Before Upload using Ajax- HDTuto.com</title>

        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.1.1/css/bootstrap.min.css">

        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/croppie/2.6.2/croppie.min.css">

        <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

        <script src="https://cdnjs.cloudflare.com/ajax/libs/croppie/2.6.2/croppie.js"></script>

        <meta name="csrf-token" content="{{ csrf_token() }}">

    </head>



    <body>

    <div class="container">

        <div class="panel panel-info">

            <div class="panel-heading">Laravel 5.6 - Preview and Crop Image Before Upload using Ajax- HDTuto.com</div>

            <div class="panel-body">



                <div class="row">

                    <div class="col-md-4 text-center">

                        <div id="upload-demo"></div>

                    </div>

                    <div class="col-md-4" style="padding:5%;">

                        <strong>Select image to crop:</strong>

                        <input type="file" id="image">



                        <button class="btn btn-primary btn-block upload-image" style="margin-top:2%">Upload Image</button>

                    </div>



                    <div class="col-md-4">

                        <div id="preview-crop-image" style="background:#9d9d9d;width:300px;padding:50px 50px;height:300px;"></div>

                    </div>

                </div>



            </div>

        </div>

    </div>



    <script type="text/javascript">



        $.ajaxSetup({

            headers: {

                'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')

            }

        });



        var resize = $('#upload-demo').croppie({

            enableExif: true,

            enableOrientation: true,

            viewport: {

                width: 200,

                height: 200,

                type: 'circle'

            },

            boundary: {

                width: 300,

                height: 300

            }

        });



        $('#image').on('change', function () {

            var reader = new FileReader();

            reader.onload = function (e) {

                resize.croppie('bind',{

                    url: e.target.result

                }).then(function(){

                    console.log('jQuery bind complete');

                });

            }

            reader.readAsDataURL(this.files[0]);

        });



        $('.upload-image').on('click', function (ev) {

            resize.croppie('result', {

                type: 'canvas',

                size: 'viewport'

            }).then(function (img) {

                $.ajax({

                    url: "{{route('upload.image')}}",

                    type: "POST",

                    data: {"image":img},

                    success: function (data) {

                        html = '<img src="' + img + '" />';

                        $("#preview-crop-image").html(html);

                    }

                });

            });

        });



    </script>



    </body>

    </html>


</p>


























