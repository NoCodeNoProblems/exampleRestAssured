# exampleRestAssured

``` java
@Test
public void creditCardsCreateTest() throws InterruptedException, JsonProcessingException {//@formatter:off
		Customer customer = new BuilderCustomer()
				.name("Tokio Marine Test")
				.build();
		CreditCard creditcard = new BuilderCreditCard()
				.customer(customer)
				.brand(Brand.VISA)
				.cvv("399")
				.expMonth(8)
				.expYear(2019)
				.holder("Tokio Marine Test")
				.number("4556379742764523")
				.build();

		ObjectMapper mapper = new ObjectMapper();
				given()
				.auth()
				.basic("admin", "admin")
				.contentType("application/json")
				.body(mapper.writeValueAsString(creditcard))
				.when()
				.post("v1/credit-cards")
				.then()
				.statusCode(201)
				.body("brand", equalTo(Brand.VISA.toString()))
				.body("cvv", equalTo("399"))
				.body("holder", equalTo("Tokio Marine Test")).log().all();
	}
```
