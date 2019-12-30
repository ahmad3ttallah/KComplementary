# KComplementary
Algorithm to find pairs in which the sum of both is equal to a given value.

    Consider all possible corner cases.
# e.g

    a = [1, 8, -3, 0, 1, 3, -2, 4, 5]
    k = 6

    count = 7
    
    a = [1, 5, 3, 4, 2]
    k = 3

    count = 7
    
    a = [1, 1, 1, 1]
    k = 2

    count = 16 
    
----------------------------------------------------------------------------------------------------
    
# Solution

    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;


    public class KComplementary
    {
        public static void main(String[] args)
        {
            int[] arr = new int[] {1, 8, -3, 0, 1, 3, -2, 4, 5};
            int k = 6;

            int result = getPairs(k, arr);
            System.out.println("result : " + result);

            arr = new int[] {1, 5, 3, 4, 2};
            k = 3;

            result = getPairs(k, arr);
            System.out.println("result : " + result);

            arr = new int[] {1, 1, 1, 1};
            k = 2;

            result = getPairs(k, arr);
            System.out.println("result : " + result);
        }

        static int getPairs(int k, int arr[])
        {
            Map<Integer, List<Integer>> map = new HashMap<>();
            int count = 0;
            for (int i = 0; i < arr.length; i++)
            {
                List<Integer> list = map.get(arr[i]);
                if (list != null)
                {
                    list.add(i);
                }
                else
                {
                    list = new ArrayList<>(Arrays.asList(i));
                }

                map.put(arr[i], list);

                int remain = k - arr[i];
                if (map.containsKey(remain))
                {
                    System.out.print("(" + map.get(remain) + ", " + i + ")" + " ");

                    if (map.get(remain).contains(i))
                    {
                        count = count + 1 + (map.get(remain).size() - 1) * 2;
                    }
                    else
                    {
                        count = count + map.get(remain).size() * 2;
                    }
                }
            }
            return count;
        }
    }
