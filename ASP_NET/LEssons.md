1. If you want to get values from appsettings.json, make sure you have same property name in the model ,
   For example :
   "GoogleReCAPTCHA": {
   "SiteKey": "6Le3RZkkAAAAAJk_luai8sQUyYegCaU-rojAdcsx",
   "SecretKey": "6Le3RZkkAAAAAGR3nJj3ZB_ISol653-5t0rC4SPO"
   },\
   if you have this as a section in your appsettings.json ....
   then the model should be ...........
   public class ReCAPTCHAsettings
   {
   public string SiteKey { get; set; } = String.Empty;
   public string SecretKey { get; set; } = String.Empty;
   }
