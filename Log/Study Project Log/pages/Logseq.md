- ```clojure
  #+BEGIN_QUERY
  {
  :query ( page-property :team )
  }
  #+END_QUERY
  ```
- ```clojure
  #+BEGIN_QUERY
  {
  :query (page-tags <% current page %> )
  }
  #+END_QUERY
  ```
- ```clojure
  #+BEGIN_QUERY
  {
  :query ( and (page-tags Library) (page-tags Causality) )
  }
  #+END_QUERY
  ```