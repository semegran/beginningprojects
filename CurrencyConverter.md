import java.util.ArrayList;
import andrew.paulman.io.Keyboard;

enum CurrencyType
{
	usd, pound, euro
}

public class CurrencyDriver 
{
	public static void main(String[] args) 
	{
		runCurrencyConversion();
	}
	/**
	 * 
	 */
	public static void runCurrencyConversion()
	{
		System.out.println("Currency Converter");
		System.out.println("");
		ArrayList <String> validResponses = new ArrayList <String> ();
		validResponses.add("u");
		validResponses.add("p");
		validResponses.add("e");
		String prompt = "Please Select The Currency To Convert From = (u = usd, p = pound, e = euro)";
		String warning = "This Is An Invalid Key. Please Try Again.";
		String convertFrom = getValidKeyTyped (prompt, warning, validResponses);
		prompt = "Please Select The Currency To Convert To = (u = usd, p = pound, e = euro)";
		String convertTo = getValidKeyTyped (prompt, warning, validResponses);
		System.out.println("Please Enter The Amount To Be Converted: ");
		double currency= Keyboard.readDouble();
		CurrencyType eTo = convertStringToCurrencyType (convertFrom);
		CurrencyType eFrom = convertStringToCurrencyType (convertTo);
		double convertedCurrency = currencyConverter (currency, eTo, eFrom /*why different when switch*/);
		System.out.println("You would have " + convertedCurrency);
		
	}
	
	public static CurrencyType convertStringToCurrencyType (String stringCurrency)
	{
		CurrencyType typeOfCurrency;
		if (stringCurrency.equals("u"))
		{
			typeOfCurrency = CurrencyType.usd;
		}
		else if (stringCurrency.equals("p"))
		{
			typeOfCurrency = CurrencyType.pound;
		}
		else 
		{
			typeOfCurrency = CurrencyType.euro;
		}
		return typeOfCurrency;
	}
	
	/**
	 * Converts one currency to another.
	 * 
	 * @param currencyAmountToBeConverted The amount of money in the old currency
	 * @return The amount of money in the new currency
	 */
	public static double currencyConverter (double currency, CurrencyType from, CurrencyType to)
	{
		double convertedCurrency = currency;
		
		if (from == CurrencyType.usd)
		{
			if (to == CurrencyType.pound)
			{
				convertedCurrency = currency * 0.75508;
			}
			else if (to == CurrencyType.euro)
			{
				convertedCurrency = currency * 0.908012;
			}
		}	
		else if (from == CurrencyType.pound)
		{	
			if (to == CurrencyType.usd)
			{
				convertedCurrency = currency * 1.32436;
			}
			else if (to == CurrencyType.euro)
			{
				convertedCurrency = currency * 1.20291;
			}	
		}	
		else 
		{
			if (to == CurrencyType.usd)
			{
				convertedCurrency = currency * 1.10131;
			}
			
			else if (to == CurrencyType.pound)
			{
				convertedCurrency = currency * 0.83132;	
			}
		}
		return convertedCurrency;
	}
	
	public static String getValidKeyTyped (String prompt, String warning, ArrayList <String> validResponses)
	{
		boolean isValidResponse = false;
		String userInput = "";
		while (isValidResponse == false)
		{
			System.out.println(prompt);
			userInput = Keyboard.readString();
			if (isValidKeyTyped(userInput, validResponses))
			{
				isValidResponse = true;
			}
			else 
			{
				System.out.println(warning);
			}
		}
		return userInput.substring(0,1).toLowerCase();
	}
  
	public static boolean isValidKeyTyped (String userInput, ArrayList <String> validResponses)
	{
		boolean isValidKey = false;
		for (String validResponse: validResponses)
		{
			if (validResponse.equals(userInput.substring(0,1)))
			{
				isValidKey = true;
				break;		
			}
		}
		return isValidKey;
	}
}
