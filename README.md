
###  DATE: 

###  NAME: kavisree.s
###  ROLL NO :212222047001
###  DEPARTMENT: BE CSE

# EXPERIMENT--04-INTERFACING IOT DEVELOPMENT BOARD AND CONFIGURE USART FOR TRANSFERRING STRINGS 
## Aim: To Interface iot development board for configuring the the usart and transfer strings though it 
## Components required: STM32 CUBE IDE, ARM IOT development board,  STM programmer tool, Serial port utility tool 
## Theory 
The full form of an ARM is an advanced reduced instruction set computer (RISC) machine, and it is a 32-bit processor architecture expanded by ARM holdings. The applications of an ARM processor include several microcontrollers as well as processors. The architecture of an ARM processor was licensed by many corporations for designing ARM processor-based SoC products and CPUs. This allows the corporations to manufacture their products using ARM architecture. Likewise, all main semiconductor companies will make ARM-based SOCs such as Samsung, Atmel, TI etc.


1.select the appropriate pins as gipo, in or out, USART or required options and configure 
![image](https://user-images.githubusercontent.com/36288975/226189403-f7179f1a-3eae-4637-826b-ab4ec35ba1e1.png)
![image](https://user-images.githubusercontent.com/36288975/226189425-2b2414ce-49b3-4b61-a260-c658cb2e4152.png)
configure in the usart 2 as asynchronous mode and set the baud rate as 115200 as shown below 
![image](https://user-images.githubusercontent.com/36288975/234776631-d6a84ef4-904c-4eac-98ed-ab6253e9379c.png)

  
2.click on cntrl+S , automaticall C program will be generated 
![image](https://user-images.githubusercontent.com/36288975/226189443-8b43451d-0b14-47e4-a20b-cc09c6ad8458.png)
![image](https://user-images.githubusercontent.com/36288975/226189450-85ffa969-2ffb-4788-81e5-72d60fdda0f1.png)
8. edit the program and as per required 
![image](https://user-images.githubusercontent.com/36288975/226189461-a573e62f-a109-4631-a250-a20925758fe0.png)

3. use project and build all 
![image](https://user-images.githubusercontent.com/36288975/226189554-3f7101ac-3f41-48fc-abc7-480bd6218dec.png)
10. once the project is bulild 
![image](https://user-images.githubusercontent.com/36288975/226189577-c61cc1eb-3990-4968-8aa6-aefffc766b70.png)

4. click on debug option 
![image](https://user-images.githubusercontent.com/36288975/226189625-37daa9a3-62e9-42b5-a5ce-2ac63345905b.png)

5 connect the  ARM board to power supply and usb 


6. check for execution of the output using run option
7. Opend serial port utility and check the outpu t



## STM 32 CUBE PROGRAM :
#include "main.h" 
#if defined (__ICCARM__) || defined (__ARMCC_VERSION)  
#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)  
#elif defined(__GNUC__)  
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)  
#endif /* __ICCARM__ || __ARMCC_VERSION */   
UART_HandleTypeDef huart2;  
void SystemClock_Config(void);  
static void MX_GPIO_Init(void);  
static void MX_USART2_UART_Init(void);  

int main(void)    
{  
 
  HAL_Init();   
  SystemClock_Config();  
  MX_GPIO_Init();  
  MX_USART2_UART_Init();  
  while (1)  
  {   
	  printf("kavisree\n");   
	  HAL_Delay(500);  
  }  
  
}   
PUTCHAR_PROTOTYPE   
{  

  HAL_UART_Transmit(&huart2, (uint8_t *)&ch, 1, 0xFFFF);   

  return ch;   
}  
void SystemClock_Config(void)  
{  
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};   
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};   
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);  
  
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_MSI;   
  RCC_OscInitStruct.MSIState = RCC_MSI_ON;   
  RCC_OscInitStruct.MSICalibrationValue = RCC_MSICALIBRATION_DEFAULT;   
  RCC_OscInitStruct.MSIClockRange = RCC_MSIRANGE_6;   
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;  
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)  
  {  
    Error_Handler();  
  }   
  
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK3|RCC_CLOCKTYPE_HCLK   
                              |RCC_CLOCKTYPE_SYSCLK|RCC_CLOCKTYPE_PCLK1   
                              |RCC_CLOCKTYPE_PCLK2;  
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_MSI;   
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;  
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;   
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;    
  RCC_ClkInitStruct.AHBCLK3Divider = RCC_SYSCLK_DIV1;   

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)   
  {  
    Error_Handler();  
  }  
}   

static void MX_USART2_UART_Init(void)   
{  
  huart2.Instance = USART2;  
  huart2.Init.BaudRate = 115200;  
  huart2.Init.WordLength = UART_WORDLENGTH_8B;   
  huart2.Init.StopBits = UART_STOPBITS_1;  
  huart2.Init.Parity = UART_PARITY_NONE;   
  huart2.Init.Mode = UART_MODE_TX_RX;   
  huart2.Init.HwFlowCtl = UART_HWCONTROL_NONE;  
  huart2.Init.OverSampling = UART_OVERSAMPLING_16;   
  huart2.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE;   
  huart2.Init.ClockPrescaler = UART_PRESCALER_DIV1;  
  huart2.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT;  
  if (HAL_UART_Init(&huart2) != HAL_OK)  
  {  
    Error_Handler();   
  }  
  if (HAL_UARTEx_SetTxFifoThreshold(&huart2, UART_TXFIFO_THRESHOLD_1_8) != HAL_OK)  
  {  
    Error_Handler();  
  }  
  if (HAL_UARTEx_SetRxFifoThreshold(&huart2, UART_RXFIFO_THRESHOLD_1_8) != HAL_OK)  
  {  
    Error_Handler();   
  }   
  if (HAL_UARTEx_DisableFifoMode(&huart2) != HAL_OK)   
  {   
    Error_Handler();   
  }  
}  

static void MX_GPIO_Init(void)   
{   
  __HAL_RCC_GPIOA_CLK_ENABLE();   

}   
void Error_Handler(void)   
{   
  __disable_irq();   
  while (1)   
  {   
  }   
 
}  

#ifdef  USE_FULL_ASSERT   

void assert_failed(uint8_t *file, uint32_t line)   
{   
  
}   
#endif  



## Output screen shots of Serial port utility   :
![image](https://github.com/kavisree86/-EXPERIMENT--03-INTERFACE-IOT-BOARD-AND-CONFIGURE-USART-TO-TRANSFER-STRINGS-/assets/145759687/c190072b-3886-4e05-bd48-dde426c4f6f0)

 
 
 
 
## Result :
configuring and usart is accomplished and string data is visualized on the serial port utilty
