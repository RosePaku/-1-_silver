# 라이브러리
library(shiny);library(shinydashboard);library(tidyverse)
# install.packages("shinydashboardPlus")
library(shinydashboardPlus);library(dplyr);library(tidyr);library(ggplot2);library(plotly);library(readxl);library(plyr);library(stringr)
# install.packages("shinyjs")
library(shinyjs)

# 고혈압 인구 통계 전처리 데이터
# load("hbp_pop_pro.RData")
load("silver_rdata/hbp_pop_pro.RData")

# 고혈압 지역 통계 전처리 데이터
load("silver_rdata/hbp_area_pro.RData")
# 치매 인구 통계
load("silver_rdata/silver_dem_pop_pro_1159.RData") # 기달
# 치매 지역 통계
load("silver_rdata/silver_area_dem_1107.RData") 
# 당뇨 지역 통계
load("silver_rdata/silver_dm_pop_pro_1159.RData")
# 당뇨 인구 통계
load("silver_rdata/silver_area_dm_1107.RData") 

# setwd("~/Desktop/my_folder")
# setwd("C:/guro/guro_01/SpyderBD_01/data/guro_01/shiny01/data/shiny_pop/silver_rdata/")
# getwd()
# -------------------------------------------------------------
# 인터랙티브 시각화 / 다시 확인

# 1
ggplotly(hbp_pop_ggplot)
# 2
ggplotly(hbp_pop_ggplot_male)
ggplotly(hbp_pop_ggplot_female)
# 3
hbp_sal_ggplot

#----------------------------------------------------------
#----------------------------------------------------------
#----------------------------------------------------------
#----------------------------------------------------------
#----------------------------------------------------------
#----------------------------------------------------------
# 1. 샤이니 앱 시작
ui <- dashboardPage( # 유아이
  
  dashboardHeader(
    title = "4조 실버"
  )#대시보드 헤더 마지막
  ,
  
  
  #----------------------------------------------------------
  # 대시보드바
  
  
  dashboardSidebar(
    
    
    
    tags$head(tags$style(HTML('.shiny-server-account { display: none; }'))),
    selectInput("region", HTML("2018-2021년도 <br> 만성 질환 카테고리"),
                choices = c("고혈압", "치매", "당뇨")),
    
    tags$head(tags$style(HTML('.shiny-server-account { display: none; }'))),
    selectInput("sex", HTML("세부 카테고리"),
                choices = c("성별/연령", "지역")),
    
    actionButton("category1_all", "초기화 "),
    
    
    
    
    
    conditionalPanel(
      condition = "input.region == '고혈압' & input.sex == '성별/연령'",
      checkboxInput("hbp_pop_checkbox1", "연도에 따른 내원일수 추이(남성)"),
      checkboxInput("hbp_pop_checkbox2", "연도에 따른 내원일수 추이(여성)"),
      checkboxInput("hbp_pop_checkbox3", "연도별 요양급여 비용총액 추이"),
      checkboxInput("hbp_pop_checkbox4", "2018년~2021년 요양급여 비용총액 비율"),
      checkboxInput("hbp_pop_checkbox5", "요약통계량")
    ) #성별&연령 고혈압 체크박스 조건문 1-1
    ,
    
    
    
    
    conditionalPanel(
      condition = "input.region == '고혈압' & input.sex == '지역'",
      checkboxInput("hbp_area_checkbox1", "연도별 요양급여비용총액 추이"),
      checkboxInput("hbp_area_checkbox2", "요양기관소재지별 요양급여비용총액"),
      checkboxInput("hbp_area_checkbox3", "연도에 따른 요양기관 소재지별 내원일수 추이"),
      checkboxInput("hbp_area_checkbox4", "2018년~2021년 총계 요약통계량")
    ) # 지역 고혈압 체크박스 조건문 1-2
    ,
    
    
    conditionalPanel(
      condition = "input.region == '치매' & input.sex == '성별/연령'",
      checkboxInput("dem_pop_checkbox1", "연도에 따른 내원일수 추이(남성)"),
      checkboxInput("dem_pop_checkbox2", "연도에 따른 내원일수 추이(여성)"),
      checkboxInput("dem_pop_checkbox3", "연도별 요양급여 비용총액 추이"),
      checkboxInput("dem_pop_checkbox4", "2018년~2021년 요양급여 비용총액 비율"),
      checkboxInput("dem_pop_checkbox5", "요약통계량")
    ) # 성별/연령 치매 체크박스 조건문 2-1
    ,
    
    conditionalPanel(
      condition = "input.region == '치매' & input.sex == '지역'",
      checkboxInput("dem_area_checkbox1", "연도별 요양급여비용총액 추이"),
      checkboxInput("dem_area_checkbox2", "요양기관소재지별 요양급여비용총액"),
      checkboxInput("dem_area_checkbox3", "연도에 따른 요양기관 소재지별 내원일수 추이"),
      checkboxInput("dem_area_checkbox4", "요약통계량") 
      
    ),# 지역 치매 체크박스 조건문 2-2
    
    
    conditionalPanel(
      condition = "input.region == '당뇨' & input.sex == '성별/연령'",
      checkboxInput("dm_pop_checkbox1", "연도에 따른 내원일수 추이(남성)"),
      checkboxInput("dm_pop_checkbox2", "연도에 따른 내원일수 추이(여성)"),
      checkboxInput("dm_pop_checkbox3", "연도별 요양급여 비용총액 추이"),
      checkboxInput("dm_pop_checkbox4", "2018년~2021년의 요양급여 비용총액 비율"),
      checkboxInput("dm_pop_checkbox5", "요약통계량"),
      
    ), # 성별/연령 당뇨 체크박스 조건문 3-1
    
    
    conditionalPanel(
      condition = "input.region == '당뇨' & input.sex == '지역'",
      checkboxInput("dm_area_checkbox1", "연도별 요양급여비용총액 추이  "),
      checkboxInput("dm_area_checkbox2", "요양기관소재지별 요양급여비용총액"),
      checkboxInput("dm_area_checkbox3", "연도에 따른 요양기관 소재지별 내원일수 추이"),
      checkboxInput("dm_area_checkbox4", "요약통계량"),
      
    ) # 지역 당뇨 체크박스 조건문 3-2 
    
    
    
    
  )# 대시보드사이드바 마지막
  ,
  
  
  dashboardBody(
    h3(""),
    uiOutput("info"),
    # div(class = "bottom-div", "Chicken123")
    # Add this output element
    verbatimTextOutput("summary_stats")
    
    
    
  ) #대시보드바디 마지막
  
  
  
)#대시보드페이지 마지막




#---------------------------------------------------------
#---------------------------------------------------------
#----------------------------------------------------------
# 서버

server <- function(input, output, session) {
  
  
  observeEvent(input$category1_all, {
    updateCheckboxInput(session, "hbp_pop_checkbox1", value = FALSE)
    updateCheckboxInput(session, "hbp_pop_checkbox2", value = FALSE)
    updateCheckboxInput(session, "hbp_pop_checkbox3", value = FALSE)
    updateCheckboxInput(session, "hbp_pop_checkbox4", value = FALSE)
    updateCheckboxInput(session, "hbp_pop_checkbox5", value = FALSE)
    updateCheckboxInput(session, "hbp_area_checkbox1", value = FALSE)
    updateCheckboxInput(session, "hbp_area_checkbox2", value = FALSE)
    updateCheckboxInput(session, "hbp_area_checkbox3", value = FALSE)
    updateCheckboxInput(session, "hbp_area_checkbox4", value = FALSE)
    # 고혈압 체크박스 초기화 (버튼 기능)
    
    updateCheckboxInput(session, "dem_pop_checkbox1", value = FALSE)
    updateCheckboxInput(session, "dem_pop_checkbox2", value = FALSE)
    updateCheckboxInput(session, "dem_pop_checkbox3", value = FALSE)
    updateCheckboxInput(session, "dem_pop_checkbox4", value = FALSE)
    updateCheckboxInput(session, "dem_pop_checkbox5", value = FALSE)
    updateCheckboxInput(session, "dem_area_checkbox1", value = FALSE)
    updateCheckboxInput(session, "dem_area_checkbox2", value = FALSE)
    updateCheckboxInput(session, "dem_area_checkbox3", value = FALSE)
    updateCheckboxInput(session, "dem_area_checkbox4", value = FALSE)
    # 치매 체크박스 초기화 (버튼 기능)
    
    updateCheckboxInput(session, "dm_pop_checkbox1", value = FALSE)
    updateCheckboxInput(session, "dm_pop_checkbox2", value = FALSE)
    updateCheckboxInput(session, "dm_pop_checkbox3", value = FALSE)
    updateCheckboxInput(session, "dm_pop_checkbox4", value = FALSE)
    updateCheckboxInput(session, "dm_pop_checkbox5", value = FALSE)
    updateCheckboxInput(session, "dm_area_checkbox1", value = FALSE)
    updateCheckboxInput(session, "dm_area_checkbox2", value = FALSE)
    updateCheckboxInput(session, "dm_area_checkbox3", value = FALSE)
    updateCheckboxInput(session, "dm_area_checkbox4", value = FALSE)
    # 당뇨 체크박스 초기화 (버튼 기능)
    
  })
  
  
  # 고혈압 1 ---------------------------------------------------------
  
  output$info <- renderUI({
    if(input$region == "고혈압" & input$sex == "성별/연령" ) {
      h4("North America")
      p("Information about North America")
      
      # 고혈압 체크박스 인풋 입력값
      checkboxes_selected <- c(input$hbp_pop_checkbox1, input$hbp_pop_checkbox2,input$hbp_pop_checkbox3,input$hbp_pop_checkbox4,input$hbp_pop_checkbox5)
      
      # 체크박스 리스트
      plots_list <- list()
      
      
      if (checkboxes_selected[1]) {
        plots_list[[1]] <- ggplotly(hbp_pop_ggplot_male)
      } # 고혈압 체크박스 조건문 1
      if (checkboxes_selected[2]) {
        plots_list[[2]]  <- ggplotly(hbp_pop_ggplot_female)
      } # 고혈압 체크박스 조건문 2
      if (checkboxes_selected[3]) {
        plots_list[[3]] <- ggplotly(hbp_pop_ggplot)
      } # 고혈압 체크박스 조건문 3
      if (checkboxes_selected[4]) {
        plots_list[[4]] <- hbp_sal_ggplot
      } # 고혈압 체크박스 조건문 4 
      if (input$hbp_pop_checkbox5) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          hbp_pop_summary
        }))# 고혈압 요약통계량
        
        plots_list[[5]] <- output_list
        
      }
      
      
      
      # 고혈압 체크박스 조건문 5 (요약통계)
      
      
      #리턴 반환문
      do.call(tagList, plots_list)
      
    } # 고혈압 조건문  (고혈압/성별&연령) 1-1
    
    #------------------------------------------------------------------
    #------------------------------------------------------------------
    
    else if(input$region == "고혈압" & input$sex == "지역" ) {
      h4("North America")
      p("Information about North America")
      
      # 고혈압 체크박스 인풋 입력값
      checkboxes_selected <- c(input$hbp_area_checkbox1, input$hbp_area_checkbox2,input$hbp_area_checkbox3,input$hbp_area_checkbox4)
      
      # 체크박스 리스트
      plots_list <- list()
      
      
      if (checkboxes_selected[1]) {
        plots_list[[1]] <- hbp_area_year_sal_ggplot
      } # 지역 고혈압 체크박스 조건문 1 (연도별 요양급여비용총액 추이)
      
      if (checkboxes_selected[2]) {
        plots_list[[2]]  <- hbp_area_hospital_ggplot
      } # 지역 고혈압 체크박스 조건문 2 (요양기관소재지별 요양급여비용총액)
      
      if (checkboxes_selected[3]) {
        plots_list[[3]] <- hbp_area_sal_ggplot
      } # 지역 고혈압 체크박스 조건문 3 (연도에 따른 요양기관 소재지별 내원일수 추이)
      
      
      if (input$hbp_area_checkbox4) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          hbp_area_summary
        }))# 고혈압 요약통계량
        
        plots_list[[4]] <- output_list
        
      }
      
      
      
      # 지역 고혈압 체크박스 조건문 4 (요약 통계량)
      
      
      #리턴 반환문
      do.call(tagList, plots_list)
      
    } # 고혈압 조건문  (고혈압/지역) 1-2
    
    
    # 치매 2 -------------------------------------------------------------
    # 치매 2 성별/연령 pop
    
    
    else if(input$region == "치매" & input$sex == "성별/연령" ) {
      h4("North America")
      p("Information about North America")
      
      # 치매 체크박스 인풋 입력값
      checkboxes_selected <- c(input$dem_pop_checkbox1, input$dem_pop_checkbox2,input$dem_pop_checkbox3,input$dem_pop_checkbox4,input$dem_pop_checkbox5)
      
      # 체크박스 리스트
      plots_list2 <- list()
      
      
      if (checkboxes_selected[1]) {
        plots_list2[[1]] <- dem_p_male_ggplot_inter
      } # 치매 체크박스 조건문 1 # 연도에 따른 내원일 수 추이 (남)
      if (checkboxes_selected[2]) {
        plots_list2[[2]]  <- dem_p_female_ggplot_inter
      } # 치매 체크박스 조건문 2 # 연도에 따른 내원일 수 추이 (녀)
      if (checkboxes_selected[3]) {
        plots_list2[[3]] <- dem_pop_ggplot_inter
      } # 치매 체크박스 조건문 3 # 연도별 요양급여 비용총액 추이
      if (checkboxes_selected[4]) {
        plots_list2[[4]] <- dem_p_sal_ggplot
      } # 치매 체크박스 조건문 4 # 2018년~2021년 요양급여 비용총액 비율
      if (input$dem_pop_checkbox5) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          dem_p_summary
        }))# 치매 요약통계량
        
        plots_list2[[5]] <- output_list
        
      }
      
      
      
      # 치매 체크박스 조건문 5 (요약통계)
      
      
      #리턴 반환문
      do.call(tagList, plots_list2)
      
    } # 치매 조건문  (성별&연령) 2-1
    
    #------------------------------------------------------------------
    #------------------------------------------------------------------
    
    else if(input$region == "치매" & input$sex == "지역" ) {
      h4("North America")
      p("Information about North America")
      
      # 치매 체크박스 인풋 입력값
      checkboxes_selected <- c(input$dem_area_checkbox1, input$dem_area_checkbox2,input$dem_area_checkbox3,input$dem_area_checkbox4)
      
      # 체크박스 리스트
      plots_list2 <- list()
      
      # !!!!!!!!!
      if (checkboxes_selected[1]) {
        plots_list2[[1]] <- dem_area_ggplot_inter 
      } # 지역 치매 체크박스 조건문 1 (연도별 요양급여비용총액 추이)
      
      if (checkboxes_selected[2]) {
        plots_list2[[2]]  <- dem_area_hospital_ggplot_inter
      } # 지역 치매 체크박스 조건문 2 (요양기관소재지별 요양급여비용총액)
      
      if (checkboxes_selected[3]) {
        plots_list2[[3]] <- dem_area_sal_ggplot_inter
      } # 지역 치매 체크박스 조건문 3 (연도에 따른 요양기관 소재지별 내원일수 추이)
      
      
      if (input$dem_area_checkbox4) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          dem_area_summary
        }))# 치매 요약통계량
        
        plots_list2[[4]] <- output_list
        
      }
      
      
      
      # 지역 치매 체크박스 조건문 4 (요약 통계량)
      
      
      #리턴 반환문
      do.call(tagList, plots_list2)
      
    } # 치매 조건문  (지역) 2-2
    
    
    
    # 치매 끝-------------------------------------------------------------
    
    
    # 당뇨 3 시작 -------------------------------------------------------------
    # 당뇨 3 성별/연령 pop
    
    
    else if(input$region == "당뇨" & input$sex == "성별/연령" ) {
      h4("North America")
      p("Information about North America")
      
      # 당뇨 체크박스 인풋 입력값
      checkboxes_selected <- c(input$dm_pop_checkbox1, input$dm_pop_checkbox2,input$dm_pop_checkbox3,input$dm_pop_checkbox4,input$dm_pop_checkbox5)
      
      # 체크박스 리스트
      plots_list2 <- list()
      
      # 수정하기 0323 // 23:47분 (23시)
      
      if (checkboxes_selected[1]) {
        plots_list2[[1]] <- dm_p_male_ggplot_inter
      } # 당뇨 체크박스 조건문 1 # 연도에 따른 내원일 수 추이 (남)
      if (checkboxes_selected[2]) {
        plots_list2[[2]]  <- dm_p_female_ggplot_inter
      } # 당뇨 체크박스 조건문 2 # 연도에 따른 내원일 수 추이 (녀)
      if (checkboxes_selected[3]) {
        plots_list2[[3]] <- dm_pop_ggplot_inter
      } # 당뇨 체크박스 조건문 3 # 연도별 요양급여 비용총액 추이
      if (checkboxes_selected[4]) {
        plots_list2[[4]] <- dm_p_sal_ggplot
      } # 당뇨 체크박스 조건문 4 # 2018년~2021년 요양급여 비용총액 비율
      if (input$dm_pop_checkbox5) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          dm_p_summary
        }))# 당뇨 요약통계량
        
        plots_list2[[5]] <- output_list
        
      }
      
      
      
      # 당뇨 체크박스 조건문 5 (요약통계)
      
      
      #리턴 반환문
      do.call(tagList, plots_list2)
      
    } # 당뇨 조건문  (성별&연령) 2-1
    
    #------------------------------------------------------------------
    #------------------------------------------------------------------
    
    else if(input$region == "당뇨" & input$sex == "지역" ) {
      h4("North America")
      p("Information about North America")
      
      # 당뇨 체크박스 인풋 입력값
      checkboxes_selected <- c(input$dm_area_checkbox1, input$dm_area_checkbox2,input$dm_area_checkbox3,input$dm_area_checkbox4)
      
      # 체크박스 리스트
      plots_list2 <- list()
      
      # !!!!!!!!!
      if (checkboxes_selected[1]) {
        plots_list2[[1]] <- dm_area_ggplot_inter 
      } # 지역 당뇨 체크박스 조건문 1 (연도별 요양급여비용총액 추이)
      
      if (checkboxes_selected[2]) {
        plots_list2[[2]]  <- dm_area_hospital_ggplot_inter
      } # 지역 당뇨 체크박스 조건문 2 (요양기관소재지별 요양급여비용총액)
      
      if (checkboxes_selected[3]) {
        plots_list2[[3]] <- dm_area_sal_ggplot_inter
      } # 지역 당뇨 체크박스 조건문 3 (연도에 따른 요양기관 소재지별 내원일수 추이)
      
      
      if (input$dm_area_checkbox4) {
        output_list <- list(renderPrint({
          
          HTML(paste0(" *키워드 정의
환자수 : patient
내원일수 : hospital
청구건수 : claims
요양급여비용총액 : salary
                      
* 해당 데이터는 2018년~2021년의 성별,연령의 총 요약통계량을 산출한 결과임.
* 주목해야 할 정보는 patient, hospital, claims, salary, Insurance의 각각 최솟값, 중앙값, 최댓값임"))
          
          
        }), # 제목 타이틀
        
        renderPrint({
          dm_area_summary
        }))# 당뇨 요약통계량
        
        plots_list2[[4]] <- output_list
        
      }
      
      
      
      # 지역 당뇨 체크박스 조건문 4 (요약 통계량)
      
      
      #리턴 반환문
      do.call(tagList, plots_list2)
      
    } # 당뇨 조건문  (지역) 2-2
    
    
    
    # 당뇨 끝 -------------------------------------------------------------   
    
    
    
    
    else if(input$region == "치매") {
      h4("Europe")
      p("Information about Europe")
    } else if(input$region == "당뇨") {
      h4("Asia")
      p("Information about Asia")
    }
  }#조건문의 마지막
  )
  
  
}#서버의 마지막



#----------------------------------------------------------
# 샤이니, 서버 실행
shinyApp(ui, server)





