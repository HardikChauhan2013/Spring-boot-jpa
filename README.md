# Step 1 : 

package com.example.demo;

import javax.persistence.Entity;

import javax.persistence.GeneratedValue;

import javax.persistence.GenerationType;

import javax.persistence.Id;


@Entity

public class Category {

	@Id
	@GeneratedValue(strategy=GenerationType.AUTO)
	private int categoryId;
	
	private String categoryName;
	
	public Category() {}

	public Category(String categoryName) {
		super();
		this.categoryName = categoryName;
	}

	public int getCategoryId() {
		return categoryId;
	}

	public void setCategoryId(int categoryId) {
		this.categoryId = categoryId;
	}

	public String getCategoryName() {
		return categoryName;
	}

	public void setCategoryName(String categoryName) {
		this.categoryName = categoryName;
	}
	
	
}

# Step 2 : 

package com.example.demo;

import org.springframework.data.jpa.repository.JpaRepository;


public interface CategoryRepository 
	extends JpaRepository<Category, Integer> {
	
	

}

# Step 3 :
package com.example.demo;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.boot.CommandLineRunner;

import org.springframework.stereotype.Component;

@Component

public class ToRunCategory implements CommandLineRunner {

	
	@Autowired
	CategoryRepository cRepo;
	
	
	@Override
	public void run(String... args) throws Exception {
		
		Category c = new Category("Book");
		
		//Save category
		cRepo.save(c);
		
		//print all category
		List<Category> list =  cRepo.findAll();
		
		for (Category category : list) {
			System.out.println(category.getCategoryId());
			System.out.println(category.getCategoryName());
		}
		
		
	}

	
}


