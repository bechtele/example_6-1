Changes made in User_Interface.cpp file 
Comments are made next the the changed lines.

Changes included modifying x and y co-ordinates and names.

-------------------------------------------------

static void userInterfaceDisplayInit()
{
    displayInit();
     
    **displayCharPositionWrite ( 0,0 ); 
    displayStringWrite( "Tmp:" ); //Change from "Temperature:" to "Tmp:"

    displayCharPositionWrite ( 9,0 ); //Changed position 
    displayStringWrite( "Gas:" ); 
    
    displayCharPositionWrite ( 0,1 ); //Changed position
    displayStringWrite( "Alarm:" );
}

static void userInterfaceDisplayUpdate()
{
    static int accumulatedDisplayTime = 0;
    char temperatureString[3] = "";
    
    if( accumulatedDisplayTime >=
        DISPLAY_REFRESH_TIME_MS ) {

        accumulatedDisplayTime = 0;

        sprintf(temperatureString, "%.0f", temperatureSensorReadCelsius());
        displayCharPositionWrite ( 4,0 ); //Changed Position
        displayStringWrite( temperatureString );
        displayCharPositionWrite ( 6,0 ); //Changed Position
        displayStringWrite( "'C" );

        displayCharPositionWrite ( 13,0 ); //Changed Position

        if ( gasDetectorStateRead() ) {
            displayStringWrite( "D " ); //Changed from "Detected    " to "D "
        } else {
            displayStringWrite( "ND" ); //Changed from "Not Detected" to "ND"
        }

        displayCharPositionWrite ( 6,1 ); 
        
        if ( sirenStateRead() ) {
            displayStringWrite( "ON " );
        } else {
            displayStringWrite( "OFF" );
        }

    } else {
        accumulatedDisplayTime =
            accumulatedDisplayTime + SYSTEM_TIME_INCREMENT_MS;        
    } 
}
