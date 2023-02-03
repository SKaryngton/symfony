<style>
green { color: #299660}
yel { color: #9ea647}
blue { color: #099fc0}
red {color: #ce4141}
fs { font-size: 13px}
</style>

# [Markdown Docs](https://www.w3schools.io/file/markdown-convertpdf/) 👋 Symfony 6  [symfony](https://symfony.com/ "@embed")
___________________________________________________________
>
>  make webapp with symfony. ![image](https://cdn.path.to/some/image.jpg "This is some image...")

- ## <green>install symfony CLI


> ouvrir windows powershell
> 1. <blue>Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
> 2. <blue>irm get.scoop.sh | iex
> 3. <blue>scoop install symfony-cli</blue> <br><br>
> Tester: <br><br>
> with window powershell <br>
> <blue>symfony new my_project</blue>  <br>
> cd my_project          <br><br>
> with IDE terminal        <br>
><blue>symfony new my_project</blue>    not working <br>
><red>Problem</red>:   Symfony : die benennung "symfony" wurde nicht als Name eines cmdlet ……
><br><green>solution</green>:  composer require symfony/flex  <br>
><br><red>Problem</red>:   the openssl extension is required for ssl/tls protection but is not available. if you can not enable the openssl extension, you can disable this error, at your own risk, by setting the 'disable-tls' option to true.
><br><green>solution</green>:  composer config -g -- disable-tls true
><br><red>Problem</red>: you must enable the openssl extension in your php.ini to load information from
><br><green>solution</green>:open xampp
>1.  cliquer sur config sur la ligne apache
>2. ensuite cliquez sur <yel>PHP(php.ini)</yel>
>3. ajouter la ligne <yel>extension=php_openssl.dll</yel>
>4. puis sauvegarder
       
        
        
        

- ## <green>Update symfony CLI

><red>problem</red>:    A new Symfony CLI version is available (5.4.17, currently running 5.4.16).
><br><green>solution</green>:    with window powershell         >  <blue>scoop update symfony-cli





<br>

- ## <green>Create symfony Project

* [x] `create new project` :  <blue>symfony new app --webapp
*  [x] `run new project` 
   - <blue>symfony serve -d
   - <blue>symfony server:stop
   
   
 ## <green>create controller
  
  1.  <blue>symfony console make:controller 
      
      - `Route path`   
         - *'/blog/{id}/{name}'*
      - `Route name`  
           - *name: 'app_blog'*
      - `wildcard`    
          - *{id}  {name}*
      - `methods`
          - *methods: [GET]*
      - `wildcard constraint`  
          - *requirements: ["name"=>"[a-z]{2,10}"]*
      - `Response`  
        - **template** or **json**
      <br>

              class BlogController extends AbstractController
              {
  
              #[Route('/blog/{id}/{name}', name: 'app_blog', methods: [GET],
                requirements: ["name"=>"[a-z]{2,10}"])]
              public function index(int $id, string $name = null): Response
              {
  
              return $this->render('blog/index.html.twig', [
              'id'=>$id,
              'name' => $name,
              ]);
   
              oder
              return $this->json([
              'id'=>$id,
              'name' => $name,
              ]);

              }

## <green>Logger ( equivalent of console.log in js)

      class BlogController extends AbstractController
      {

        #[Route('/blog/{id}/{name}', name: 'app_blog']
         public function index(LoggerInterface $ logger){

        $logger->info(‘hi’);

     }
}


## <green>Twig

- **Add css path with <yel>function asset()</yel>: asset give access to the public directory**
  - <blue>composer require symfony/asset
  
        <link rel="stylesheet" href="{{ asset('styles/app.css') }}">
  
- **Generate Url with <yel>function path()**
 
      <a href="{{ path('app_homepage') }}"></a>
      
       <a href="{{ path('app_question_show', { slug: 'pausing-a-spell' }) }}"></a>
- **Heritage (block can be overridden) <yel>function extends**
        
       {% extends 'base.html.twig' %}
  
- **Inclusion  <yel>function include()** 

      {% include  ‘index.html.twig’ %}

      example

      a.html.twig

      {{ include('b.html.twig',{
      showQuestion:true
      }) }}
    
      b.html.twig

      {% if showQuestion|default(false) %}
      <a href="{{ path('app_question_show',{'slug':answer.question.slug}) }}"
      class="mb-1 link-secondary"
        >
      <strong>Question:</strong>{{ answer.question.question }}
      </a>
      {%endif %}

- **ShortText <yel>function u.truncate()**
   - <blue>composer require twig/string-extra

         {{ answer.question | u.truncate(80, '...') }}

## <green>WebpackEncore

- install node or yarn
   - <blue>yarn --version  
   - <blue>node -v
  
  <br>
  
- install <yel>Webpack
  - <blue>composer require encore

<br>

- <blue>yarn install or npm install
- <blue>yarn watch

## <green>Bootstrap Fortawesome Fontawesome(Encore)

- Install <yel>bootstrap
    - <blue>yarn add bootstrap --dev
              
           assets/styles/app.css
  
             @import '~bootstrap';

    - <blue>yarn add jquery @popperjs/core --dev

           assets/app.js
         
              require('bootstrap');

- Install <yel>Fontawesome</yel> and <yel> Fontsource
    - <blue>yarn add @fortawesome/fontawesome-free --dev  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; yarn add @fontsource/roboto-condensed --dev  

           assets/styles/app.css

             @import '~@fortawesome/fontawesome-free';
             @import '~@fontsource/roboto-condensed';
