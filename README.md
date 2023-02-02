# 👋 Symfony 6  [symfony](https://symfony.com/ "@embed")
___________________________________________________________
>
>  make webapp with symfony. ![image](https://cdn.path.to/some/image.jpg "This is some image...")

<br>

* [x] `create new project` :  symfony new app --webapp
*  [x] `run new project` 
   - symfony serve 
   - symfony server:stop
   
   
- [ ] `create controller` 
  
  1.  symfony console make:controller 
      
      - `Route path`   
         - *'/blog/{id}/{name}'*
      - `Route name`  
           - *name: 'app_blog'*
      - `wildcard`    
          - *{id}  {name}*
      - `wildcard constraint`  
          - *requirements: ["name"=>"[a-z]{2,10}"]*
      - `Response`  
        - **template** or **json**
      <br>

              class BlogController extends AbstractController
              {
  
              #[Route('/blog/{id}/{name}', name: 'app_blog',
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


  

