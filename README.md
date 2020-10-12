# maximumareahistogram
class Solution {
    vector<int> LeftSmaller(vector<int> a){
         stack<pair<int,int>> b;
        vector<int> left;
        for(int i=0;i<a.size();i++){
            if(b.size()==0){
                left.push_back(-1);
            }
            else if(b.size()>0&&b.top().first<a[i]){
                left.push_back(b.top().second);
            }
            else if(b.size()>0&&b.top().first>=a[i]){
                while(b.size()>0&&b.top().first>=a[i]){
                    b.pop();
                }
                if(b.size()==0){
                    left.push_back(-1);
                }
                else{
                    left.push_back(b.top().second);
                }
            }
            b.push({a[i],i});
        }
          for(int i=0;i<left.size();i++){
         cout<<left[i];
     }
     cout<<endl;
    return left;
}
 vector<int> RightSmaller(vector<int> a){
         stack<pair<int,int>> b;
        vector<int> left;
        for(int i=a.size()-1;i>=0;i--){
            if(b.size()==0){
                left.push_back(a.size());
            }
            else if(b.size()>0&&b.top().first<a[i]){
                left.push_back(b.top().second);
            }
            else if(b.size()>0&&b.top().first>=a[i]){
                while(b.size()>0&&b.top().first>=a[i]){
                    b.pop();
                }
                if(b.size()==0){
                    left.push_back(a.size());
                }
                else{
                    left.push_back(b.top().second);
                }
            }
              b.push({a[i],i});
        }
     reverse(left.begin(),left.end());
     for(int i=0;i<left.size();i++){
         cout<<left[i];
     }
     cout<<endl;
    return left;
}
public:
    int largestRectangleArea(vector<int>& heights) {
        if(heights.size()==0){
            return 0;
        }
        
        vector<int> left= LeftSmaller(heights);
         vector<int> right= RightSmaller(heights);
        vector<int> c(heights.size());
        for(int i=0;i<heights.size();i++){
            c[i]=((right[i]-left[i])-1)*heights[i];
        }
       return *max_element(c.begin(),c.end());
    }
};
