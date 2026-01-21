//  Rayan
//  1/20/2026
//  Basic check for adjacent bracket matching.

public class Parenthesis {

    // 
    //  Pre-condition: String s contains only (, ), {, }, [, ] 
    //  Post-condition: Returns true if each pair is correctly nested.
    //
    public static boolean isValid(String s) {
        if (s.length() % 2 != 0) return false;

        char[][] pairs = { {'(', ')'}, {'{', '}'}, {'[', ']'} };

        for (int p = 0; p < pairs.length; p++) {
            char openChar = pairs[p][0];
            char closeChar = pairs[p][1];
            boolean removed = true;

            while (removed) {
                removed = false;
                int openIndex = -1;
                for (int i = 0; i < s.length(); i++) {
                    if (s.charAt(i) == openChar) {
                        openIndex = i;
                        i = s.length(); // exit the loop
                    }
                }

                if (openIndex == -1) removed = false;
                else {
                    int closeIndex = -1;
                    for (int i = openIndex + 1; i < s.length(); i++) {
                        if (s.charAt(i) == closeChar) {
                            closeIndex = i;
                            i = s.length(); // exit the loop
                        }
                    }
                    if (closeIndex == -1) return false;
                    s = s.substring(0, openIndex) + s.substring(openIndex + 1, closeIndex) + s.substring(closeIndex + 1);
                    removed = true;
                }
            }
        }

        return s.length() == 0;
    }

    //
    //  Pre-condition: Program runs normally. 
    //  Post-condition: Outputs true or false for test cases. 
    //
    public static void main(String[] args) {
        System.out.println(isValid("{([)]}"));
    }
}
