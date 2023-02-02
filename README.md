# 👋 Symfony 6  [symfony](https://symfony.com/ "@embed")
___________________________________________________________
>
>  make webapp with symfony. ![image](https://cdn.path.to/some/image.jpg "This is some image...")

<br>

* [x] `create new project` :  symfony new app --webapp
*  [x] `run new project` 
   - symfony serve -d
   - symfony server:stop
   
   
 ## `create controller` 
  
  1.  symfony console make:controller 
      
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

## `Logger ( equivalent of console.log in js)`

      class BlogController extends AbstractController
      {

        #[Route('/blog/{id}/{name}', name: 'app_blog']
         public function index(LoggerInterface $ logger){

        $logger->info(‘hi’);

     }
}


## `Twig` 

- **Add css path with function asset(): asset give access to the public directory**
  - composer require symfony/asset
  
        <link rel="stylesheet" href="{{ asset('styles/app.css') }}">
  
- **Generate Url with function path()**
 
      <a href="{{ path('app_homepage') }}"></a>
      
       <a href="{{ path('app_question_show', { slug: 'pausing-a-spell' }) }}"></a>
- **Heritage (block can be overridden)**
        
       {% extends 'base.html.twig' %}
  
- **Inclusion** 

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

- **ShortText**
   - composer require twig/string-extra

         {{ answer.question | u.truncate(80, '...') }}

