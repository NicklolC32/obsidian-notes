date: 21-09-2026
time: 17:00
topic: Java Refresher, Records, and Enums
tags:

**UUIDs** - unique identifiers that are 36 characters long, used to identify information and resources in computer systems
```
UUID.randomUUID()
```

### Records
Declaration of a record looks like a class and it defines its members inside the brackets.
```
public record OrderSummaryDto(
	String orderId,
	String customerId,
	BigDecimal totalAmount
) {}
```

Records can have compact constructors for validation or normalisation.
They are better used for immutable data models - records just store things and shouldn't need to change the data for the consumer. *Read-only classes*
```
public record ProductDto(String sku, int quantity) {
	public ProductDto {
		if (sku == null || sku.isBlank()) {
			throw new IllegalArgumentException("...");
		}
		...
		sku = sku.trim();
	}
}
```

**Lombok** - replaces tedious, repetitive code with automated annotations e.g. getters and setters (it's a library in Java)
**@Data** - automatically places getters and setters and others in your code so you don't have to type it out
^ Lombok-style annotations using @Data etc. are better suited for mutable things as it is flexible

### Enum
- Enum is a type with unchangeable values
- It can additionally act as a constructor

```
public enum OrderStatus {
	IMPORTED(10),  // usually in uppercase
	FAILED(20),
	DELETED(30);
	
	private final int code;
	
	OrderStatus(int code) {  // constructor which just creates the enum values
		this.code = code;
	}
	
	public int code() {  // e.g. OrderStatus.IMPORTED.code() => 10
		return code;
	}
}
```

### Internal and External Data Structures
**"dto"** - a convention for *external* details 
**"model"** - a convention for *internal* details
![[Pasted image 20261007194052.png|404]]
*Domain model: an Order aggregates one Customer and one-or-more OrderItems, has an OrderStatus enum and maps to an OrderSummaryDto record; externalOrderId keeps the partner ID while orderId is our own internal ID.*
- Basically there should be a separation between external and internal data. The OrderSummaryDto is what the programmer thinks is important for the consumer to know whereas everything else is kept internal and hidden

### Domain Models
- should represent internal meaning, not external JSON structure
- only DTOs should be represented in JSON, or other formats

### Collections
- pick the correct collection for the operation you use the most and for the correct intended purpose
![[Pasted image 20261007195349.png]]

### Exception Handling: Checked vs Unchecked, Try/Catch/Finally, Custom Exceptions
- *checked* and *unchecked* exceptions will deter whether the compiler needs to handle or declare the issue
- *checked* - compiler checks at compile time and generally represent conditions that a program may need to recover from e.g. file/database errors
- *unchecked* - occur at runtime and do not need to be handled/declared
- *try/catch/finally* blocks catch a specific error and the *finally* part will always run no matter if there was an error or not
- *custom exceptions* are specifically for your domain e.g. an "OrderNotFoundException"