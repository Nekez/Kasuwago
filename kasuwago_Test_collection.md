# Kasuwago
{
	"info": {
		"_postman_id": "610de253-58d3-446f-9866-35933494c428",
		"name": "Kasuwago",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
	},
	"item": [
		{
			"name": "Generate Token",
			"event": [
				{
					"listen": "test",
					"script": {
						"id": "f9356505-3788-4107-918b-b41ae02cb8a7",
						"exec": [
							"pm.test('Token Generated', function(){",
							"    pm.response.to.have.status(200)",
							"})",
							"",
							"pm.test('Has token', function(){",
							"    const{} = pm.response.json();",
							"    pm.environment.set('token', 'access_token');",
							"    return 'access_token' in {};",
							"})"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"method": "POST",
				"header": [],
				"body": {
					"mode": "urlencoded",
					"urlencoded": [
						{
							"key": "grant_type",
							"value": "password",
							"type": "text"
						},
						{
							"key": "client_id",
							"value": "lsir-client",
							"type": "text"
						},
						{
							"key": "client_secret",
							"value": "lsir-client",
							"type": "text"
						},
						{
							"key": "username",
							"value": "admin@lsir.com",
							"type": "text"
						},
						{
							"key": "password",
							"value": "Password1",
							"type": "text"
						}
					]
				},
				"url": {
					"raw": "{{baseUrl}}/connect/token",
					"host": [
						"{{baseUrl}}"
					],
					"path": [
						"connect",
						"token"
					]
				}
			},
			"response": []
		},
		{
			"name": "Product Category",
			"event": [
				{
					"listen": "test",
					"script": {
						"id": "549bf9d0-25e7-4120-b034-c220b01e96f5",
						"exec": [
							"pm.test('Created Description', function(){",
							"    pm.response.to.have.status(200)",
							"    const {result} = pm.response.json();",
							"    pm.environment.set('productCat', result.id);",
							"})"
						],
						"type": "text/javascript"
					}
				},
				{
					"listen": "prerequest",
					"script": {
						"id": "3cfebd95-2b65-4c52-a9f8-0518446e4946",
						"exec": [
							"let date = Date.now();",
							"let name = 'Foodie' + date;",
							"pm.environment.set('nameOfDescription', name);"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{token}}",
							"type": "string"
						}
					]
				},
				"method": "POST",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": " {\"name\": \"{{nameOfDescription}}\",\n \"description\": \"All kinds of food you might think of\"\n }",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "{{baseUrl}}/api/productcategory",
					"host": [
						"{{baseUrl}}"
					],
					"path": [
						"api",
						"productcategory"
					]
				}
			},
			"response": []
		},
		{
			"name": "Get Product Desc",
			"event": [
				{
					"listen": "test",
					"script": {
						"id": "d1fa8273-0524-49de-9624-43652e2d4925",
						"exec": [
							"pm.test('Created Description', function(){",
							"    pm.response.to.have.status(200)",
							"})"
						],
						"type": "text/javascript"
					}
				}
			],
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{token}}",
							"type": "string"
						}
					]
				},
				"method": "GET",
				"header": [],
				"url": {
					"raw": "{{baseUrl}}/api/productcategory/{{productCat}}",
					"host": [
						"{{baseUrl}}"
					],
					"path": [
						"api",
						"productcategory",
						"{{productCat}}"
					]
				}
			},
			"response": []
		},
		{
			"name": "Update Product Cat",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{token}}",
							"type": "string"
						}
					]
				},
				"method": "PUT",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\n  \"id\": 10,\n  \"name\": \"Wood\",\n  \"description\": \"All kinds of wood\"\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "{{baseUrl}}/api/productcategory",
					"host": [
						"{{baseUrl}}"
					],
					"path": [
						"api",
						"productcategory"
					]
				}
			},
			"response": []
		},
		{
			"name": "Toggle Active Product Cat",
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{token}}",
							"type": "string"
						}
					]
				},
				"method": "POST",
				"header": [],
				"body": {
					"mode": "raw",
					"raw": "{\n  \"id\": 1\n//   \"Name\": \"Wood\",\n//   \"Description\": \"All kinds of wood\"\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "{{baseUrl}}/api/productcategory",
					"host": [
						"{{baseUrl}}"
					],
					"path": [
						"api",
						"productcategory"
					]
				}
			},
			"response": []
		}
	],
	"protocolProfileBehavior": {}
}
