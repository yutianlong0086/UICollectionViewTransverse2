# UICollectionViewTransverse2

#### Paging Effect
![GIF](https://github.com/yutianlong0086/UICollectionViewTransverse2/blob/master/UICollectionViewTransverse2/2-page.gif)

#### Slowing Effect
![GIF](https://github.com/yutianlong0086/UICollectionViewTransverse2/blob/master/UICollectionViewTransverse2/2-free.gif)

##  Related introduction Blog

<a href="http://blog.csdn.net/yutianlong9306/article/details/51994314">http://blog.csdn.net/yutianlong9306/article/details/51994314</a>


#### UIContainerCollectionView.h  

``` objective-c

#import <UIKit/UIKit.h>

typedef NS_ENUM(NSUInteger, WBScrollType) {

    WBScrollTypeFree ,      //自由减速效果
    WBScrollTypePage        //分页的效果
};

@interface UIContainerCollectionView : UIView

- (void)setupWithDataSource:(NSArray<id> *)dataSource pointValue:(NSValue *)pointValue;

@property (nonatomic, copy) void (^pointChangeBlock)(NSValue *pointValue);

@property (nonatomic, assign) WBScrollType scrollType;      //默认是分页的

@end

```


#### Method of use

``` objective-c

- (void)setupUI {

    WEAK_SELF();
    self.containerView = [UIContainerCollectionView new];
    //defaule is Slowing Effect
    self.containerView.scrollType = WBScrollTypeFree;
    [self.containerView setPointChangeBlock:^(NSValue *pointValue) {
    weakSelf.pointChangeBlock(pointValue);
}];

    [self.contentView addSubview:self.containerView];

    [self.containerView mas_makeConstraints:^(MASConstraintMaker *make) {
    make.top.leading.trailing.bottom.equalTo(@0);
    }];
}

- (void)setupWithDataSource:(NSArray<id> *)dataSource pointValue:(NSValue *)pointValue {
    [self.containerView setupWithDataSource:dataSource pointValue:pointValue];
}

```


