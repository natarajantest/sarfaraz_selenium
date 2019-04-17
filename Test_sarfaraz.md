# sarfaraz_selenium
FinalTest

package testing;

import java.time.Duration;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;

public class Tests {

	public static void main(String[] args) throws InterruptedException {
		WebDriver driver=new ChromeDriver();
		driver.manage().timeouts().implicitlyWait(50,TimeUnit.SECONDS);
		driver.manage().window().maximize();
		driver.get("https://demo.openemr.io/d/openemr/interface/login/login.php?site=default");
		String url=driver.getCurrentUrl();
		System.out.println(url);
		driver.findElement(By.id("authUser")).sendKeys("admin");
		driver.findElement(By.id("clearPass")).sendKeys("pass");
		driver.findElement(By.name("languageChoice")).sendKeys("English");
		driver.findElement(By.xpath("//button[@ class='btn btn-default btn-lg']")).click();
		Actions act  = new Actions(driver);
		act.moveToElement(driver.findElement(By.xpath("//div[text()='Patient/Client']"))).build().perform();
		 act
			.keyDown(Keys.CONTROL)
			.pause(Duration.ofSeconds(1))
			.build()
			.perform();
		driver.findElement(By.xpath("//div[text()='New/Search']")).click();

		driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@name='pat']")));
		driver.findElement(By.id("form_fname")).sendKeys("prasad");
		driver.findElement(By.id("form_lname")).sendKeys("jangam");
		driver.findElement(By.id("form_sex")).sendKeys("Male");
		driver.findElement(By.id("form_DOB")).sendKeys("2019-04-17");
		driver.findElement(By.id("form_fname")).sendKeys("prasad");
		driver.findElement(By.id("create")).click();
		 driver.switchTo().defaultContent();
		driver.switchTo().frame(driver.findElement(By.id("modalframe")));
		driver.findElement(By.xpath("//input[@value='Confirm Create New Patient']")).click();
		Thread.sleep(3000);
	    driver.switchTo().alert().accept();
	    driver.findElement(By.xpath("//div[@class='closeDlgIframe']")).click();
	   // driver.switchTo().frame(driver.findElement(By.name("timeout")));
	   // Actions act1=new Actions(driver);
	    act.moveToElement(driver.findElement(By.xpath("//div[@class='menuSection userSection']"))).build().perform();
	    driver.findElement(By.xpath("//ul//li[text()='Logout']")).click();

	}
}
