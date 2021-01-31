# Symfony Repository

Les repository généralisent des requetes complexes en base de données, ces requetes pouront êtres utilisées dans les controleurs par exemple.
Il faut savoir que symfony propose un repository par entité, il est possible de l'enrichir et d'ajouter des traitements de donénes sépcifiques.

## Creation du repository
Pour creer un repository il suffit de creer une nouvelle classe dans le dossier repository.

Par ex: la classe BookRepository.php dans `src/Repository`
```
class BookRepository extends ServiceEntityRepository
{
   public function __construct(ManagerRegistry $registry)
  {
    parent::__construct($registry, Training::class);
  }
    ...
}
```
