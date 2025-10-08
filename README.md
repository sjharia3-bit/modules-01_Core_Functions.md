IF CURRENT_STATUS IS "SYSTEM_READY":
    WHILE TRUE:
        USER_INPUT = READ_FROM_INPUT_BUFFER()
        
        IF USER_INPUT IS NOT NULL:
            LOG "Received command: " + USER_INPUT
            PROCESSED_DATA = Handle_Data(USER_INPUT, SYSTEM_PARAMETERS)
            
            # Further processing/Module 02 call would happen here
            FINAL_RESULT = Call_Next_Module(PROCESSED_DATA)
            
            SEND_TO_OUTPUT_HANDLER(FINAL_RESULT)
            LOG "Results sent. Status: OK"
        END IF
        
        CHECK_FOR_SHUTDOWN_SIGNAL()
    END WHILE
ELSE:
    LOG "Fatal Error: System failed to initialize. Aborting."
    EXIT_SYSTEM()
