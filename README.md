# In-memory IGC track viewer

This api is an online service that will allow users to browse information about IGC files. 
IGC is an international file format for soaring track files that are used by paragliders and gliders. 
The program will store submitted tracks in memory by saving them into Go lang data structures such as Structs, Slices, Maps etc. 
These files can be browsed later by entering the specific URL paths defined later in this README.

For the development of the IGC processing, I have been using the open source IGC library for Go: <a href="https://github.com/marni/goigc">goigc</a>



## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

The root of the Igc Api is /igcinfo/ which if you enter that path you get a 404 Not Found Error. From that root you can write the other paths to get results.


### GET     /igcinfo/api

For this get request you get meta information about the API

    {
      "uptime": <uptime>
      "info": "Service for IGC tracks."
      "version": "v1"
    }

where: <uptime> is the current uptime of the service formatted according to Duration format as specified by ISO 8601. 


### POST    /igcinfo/api/igc

You can do track registration with this request by putting in the request body the URL of the Igc File

    {
      "url": "<url>"
    }


As a response you get the ID for that track:

    {
      "id": "<id>"
    }



### GET     /igcinfo/api/igc

This request returns the array of all tracks ids as an array:
    
    [<id1>, <id2>, ...]
        


### GET     /igcinfo/api/igc/\<id\>

Returns the meta information about a given track with the provided <id>, or NOT FOUND response code with an empty body.
    
    {
        "H_date": <date from File Header, H-record>,
        "pilot": <pilot>,
        "glider": <glider>,
        "glider_id": <glider_id>,
        "track_length": <calculated total track length>
    }


### GET     /igcinfo/api/igc/\<id\>/\<field\>

Returns the single detailed meta information about a given track with the provided <id>, or NOT FOUND response code with an empty body. The response should always be a string, with the exception of the calculated track length, that should be a number.

Response will be: 

    <pilot> for pilot
    
    <glider> for glider
    
    <glider_id> for glider_id
    
    <calculated total track length> for track_length
    
    <H_date> for H_date
    


## Resources

<a href="https://github.com/marni/goigc">Go IGC library</a>


## Deployment

This api has been deployed in Heroku: https://igcapi.herokuapp.com/


## Built With

Go Language
