## Exercicio TDD DevSuperior

<h4 align="left">
 Solucionar TDD apresentado com testes integrados na camada Web
</h4>

<!--ts-->

* [Autor](#autor)
* [Tecnologias](#tecnologias)
* [Desafio](#desafio)

---

### Autor

<a href="https://www.linkedin.com/in/marcelomachado1987/">
 <img style="border-radius: 50%;" src="https://media-exp1.licdn.com/dms/image/C4E03AQEwV54JjLc-9g/profile-displayphoto-shrink_800_800/0/1621682542460?e=1626912000&v=beta&t=Ctis1Z8wFBsNtnuMhTXGp7cXWA12JyY5t9KF9rfQf58" width="100px;" alt=""/>
 <br />
<b>Marcelo Machado</b></a>
 <br />

---

### 🛠 Tecnologias

As seguintes ferramentas foram usadas na construção do projeto:

- [Spring Boot](https://spring.io/projects)
- [Java 11](https://docs.oracle.com/en/java/javase/11/)
- [Hibernate + JPA](https://hibernate.org/)
- [SQL]()
- [JUnit5](https://junit.org/junit5/)
- [Mockito](https://site.mockito.org/)

---

### 🎲 Construir API para testes

```Java
@Test
public void findAllShouldReturnAllResourcesSortedByName()throws Exception{

    ResultActions result=
    mockMvc.perform(get("/departments")
    .contentType(MediaType.APPLICATION_JSON));

    result.andExpect(status().isOk());
    result.andExpect(jsonPath("$[0].name").value("Management"));
    result.andExpect(jsonPath("$[1].name").value("Sales"));
    result.andExpect(jsonPath("$[2].name").value("Training"));
```

```Java
@Test
public void findAllShouldReturnPagedResourcesSortedByName()throws Exception{

    ResultActions result=
    mockMvc.perform(get("/employees")
    .contentType(MediaType.APPLICATION_JSON));

    result.andExpect(status().isOk());
    result.andExpect(jsonPath("$.content").exists());
    result.andExpect(jsonPath("$.content[0].name").value("Alex"));
    result.andExpect(jsonPath("$.content[1].name").value("Ana"));
    result.andExpect(jsonPath("$.content[2].name").value("Andressa"));
    }

@Test
public void insertShouldInsertResource()throws Exception{

    EmployeeDTO dto=new EmployeeDTO(null,"Joaquim","joaquim@gmail.com",1L);
    String jsonBody=objectMapper.writeValueAsString(dto);

    ResultActions result=
    mockMvc.perform(post("/employees")
    .content(jsonBody)
    .contentType(MediaType.APPLICATION_JSON)
    .accept(MediaType.APPLICATION_JSON));

    result.andExpect(status().isCreated());
    result.andExpect(jsonPath("$.id").exists());
    result.andExpect(jsonPath("$.name").value("Joaquim"));
    result.andExpect(jsonPath("$.email").value("joaquim@gmail.com"));
    result.andExpect(jsonPath("$.departmentId").value(1L));
    }    
```