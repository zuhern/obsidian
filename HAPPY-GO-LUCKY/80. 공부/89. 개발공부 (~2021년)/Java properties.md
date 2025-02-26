---
Created: Invalid date
Updated: Invalid date
---
ClassLoader loader = Thread.currentThread().getContextClassLoader();

File file = new File(loader.getResource("").getFile());

String path = file.getParent() + File.separator + "classes" + File.separator

+ "conf" + File.separator;

System.out.println(path);

prop.load(new FileInputStream(path +"irtms.properties"));