# An interesting big data problem

### Name: LiuSheng<br>
### Student ID: 1801212891
---

## 1. Inspiration
In the research metholedge course I took last module, I was attracted by other's presentation about the detection of iceberg orders in the stock markets. Although, in China’s stock market, because of the restriction of "t + 1" trading system, the stocks purchased on the same day can only be sold on the next trading day. The trading strategy proposed by auther was infeasible. But, revealing the true volumes and liquidity of the stock by using data from the FOB will improve the performance of other stock transaction strategy.

## 2. Problem description
* An iceberg order is a limit order where only a fraction of the total order size is shown in the LOB at any one time, with the remainder of volume hidden. When the peak is executed, the next part of the iceberg’s hidden volume gets displayed on the LOB. This process is repeated until the initial order is fully traded or cancelled. Traders use iceberg order to hide their true transaction purpose. But the quantative traders cares about the liquidity of the stock which reflects the transaction risk. Our goal is to detect teh iceberg orders and reveal the true market liquidity <br>
* In ShenZhen Stock Exchange, they offer the level2 data which contains the first 10 candidate data of FOB instantly, instead of snapshots per half second, which ensures the constraction of strategy. In the literation, the auther only used one stock's one week data. This may be caused by the access to the data or the calculation resource. We can use more data to get a more reliable predition of iceberg orders. <br>
* The whole stock market data of ShenZhen Stock Exchange can't be processed as the same time as the data size is so big. What's more, as time goes by, the distribution and percents of iceberg order may change. We can trancate the data to small time range, and use big data technology to process it.

## 3.The intrinsic big data properties
* There is no doubt the tick level data of stock satisfy the three porperty of big data——volume, variety and velocity.
* Tens of thousands of data will be produced by the transaction everyday. Apart from the data from FOB, we can use the data from company's financial report, finincial news websites and so on.  

## 4. Workflow
 * First of all, I need to get the access to the level2 data of stock. Fortunately, I get a chance to take internship in a quant management company, the data is easy to obtain directly from the internal database. Second, there are many strategies to detect the iceberge orders in the literature. I have read the method proposed by [HUGH L. (2013)](https://www.sierrachart.com/Download.php?Folder=SupportBoard&download=9733), which is creative and practice. Maybe more material I should read to get better understanding of the topic. <br>
* They found on GLOBEX when the displayed quantity has been filled, another portion less than or equal to the displaced quantity was then displayed, with the time priority of the initial orders and the remaining hidden volume reduced by the peak size.
 ![The process like this](/image/1.png)<br>
 So, they guessed what algorithm the GLOBEX took and fitted the parameters according to it. The result is that iceberg peak size and total volumes are discrete integers, the joint distribution in not random. The anther can predict the distribution of first appearance peak size and the total volumes. 
 ![The detecting process like this](/image/3.png)<br>
 Following the literature, I need to process the raw data first, and code for the training strategy, and test the strategy. <br>

## 5. Database
  As the data is time-series data, the time-series database is the best choice, such as Kdb+. But, as I know, the database in my company is MySQL. Maybe I need to extract the part of the data from company's database and rearange them into the Kdb+ database. 
  
---
## reference
Christensen, H. L., & Woodmansey, R. (2013). Prediction of Hidden Liquidity in the Limit Order Book of GLOBEX Futures. The Journal of Trading, 8(3), 68-95.
